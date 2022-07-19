<template>
  <main>
      <div class="container pt-5">
        <div class="row row-cols-5 ">
            <SingleCard class="col" v-for="(element, index) in cardsList"  :key="index"
                :index='index'
                :element="element" 
            />
        </div>
      </div>
  </main>
</template>

<script>
import SingleCard from './singleCard.vue'
import axios from 'axios'

export default {
  components :{
    SingleCard,
  },
  data : function(){
    return {
      cardsList : []
    }
  },
  methods : {
    getCard(){
      axios.get('https://flynn.boolean.careers/exercises/api/array/music')
      .then((result)=> {
        this.cardsList = result.data.response;
      })
    }
  },
  created(){
    this.getCard()
    console.log(this.cardsList)
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
