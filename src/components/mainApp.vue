<template>
  <main class="d-flex justify-content-center align-items-center">
      <div class="container pt-5" v-if="(loading)">
        <div class="row justify-content-center">
            <SingleCard class="col-2 me-3" v-for="(element, index) in cardsList"  :key="index"
                :index='index'
                :element="element" 
            />
        </div>
      </div>
      <LoaderApp v-if="(!loading)" />
  </main>
</template>

<script>
import SingleCard from './singleCard.vue'
import LoaderApp from './loaderApp.vue'

import axios from 'axios'

export default {
  components :{
    SingleCard,
    LoaderApp,
  },
  data : function(){
    return {
      cardsList : [],
      loading : false,
    }
  },
  methods : {
    getCard(){
      axios.get('https://flynn.boolean.careers/exercises/api/array/music')
      .then((result)=> {
        this.cardsList = result.data.response;
      })
    },
    timeOut(){
      setTimeout(()=>{
        this.loading = true
      },2000)
    }
  },
  created(){
    this.getCard()
    this.timeOut()
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
