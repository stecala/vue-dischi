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
      <div v-if="(!loading)">
          <div class="lds-dual-ring"></div>
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

.lds-dual-ring {
  display: inline-block;
  width: 80px;
  height: 80px;
}
.lds-dual-ring:after {
  content: " ";
  display: block;
  width: 64px;
  height: 64px;
  margin: 8px;
  border-radius: 50%;
  border: 6px solid #fff;
  border-color: #fff transparent #fff transparent;
  animation: lds-dual-ring 1.2s linear infinite;
}
@keyframes lds-dual-ring {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

</style>
