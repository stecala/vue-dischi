<template>
  <main class="d-flex justify-content-center align-items-center">
      <div class="container pt-5" v-if="(loader)">
        <div class="row">
            <InputsUser class="col-4 m-auto" @select="setUserSelect" :genresList="genresList" />
        </div>
        <div class="row justify-content-center">
            <SingleCard class="col-2 me-3" v-for="(element, index) in filteredCards"  :key="index"
                :index='index'
                :element="element" 
            />
        </div>
      </div>
      <LoaderApp v-if="(!loader)" />
  </main>
</template>

<script>
import SingleCard from './singleCard.vue'
import LoaderApp from './loaderApp.vue'
import InputsUser from './inputsUser.vue'
import axios from 'axios'

export default {
  components :{
    SingleCard,
    LoaderApp,
    InputsUser,
},
  data : function(){
    return {
      cardsList : [],
      filteredCards : [],
      loader : false,
      userSelected : '',
      genresList : []
    }
  },
  methods : {
    getCard(){
      axios.get('https://flynn.boolean.careers/exercises/api/array/music')
      .then((result)=> {
        this.cardsList = result.data.response
        this.filteredCards= [...this.cardsList]
        this.initGenres()
        this.timeOut()
        this.searchGenre(this.userSelected)

      })
    },
    timeOut(){
      setTimeout(()=>{
        this.loader = true
      },2000)
    },
    searchGenre(element){
        console.log(element)
        this.filteredCards= [...this.cardsList].filter((artist) => artist.genre.includes(element))  
    },
    setUserSelect(choice){
        this.userSelected = choice
        this.searchGenre(this.userSelected)
    },
    initGenres(){
        for(let i =0 ; i< this.cardsList.length; i++){
          if(!this.genresList.includes(this.cardsList[i].genre)){
            this.genresList.push(this.cardsList[i].genre)
          }
        }
        
    }
  },
  created(){
    this.getCard()
  } 
}
</script>

<style scoped lang="scss">
@import "../assets/style/variables.scss";
main{
  height: calc(100vh - 70px);
  background-color: $backgroundMain;
}



</style>
