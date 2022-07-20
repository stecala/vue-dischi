<template>
  <main class="d-flex justify-content-center align-items-center">
    <div class="container pt-5" v-if="(loader)">
      <div class="row">
        <genresUser class="col-4 m-auto" @select="setUserSelect" :genresList="genresList" />
        <authorsUser class="col-4 m-auto" @selectAuthor="authorSelect" :authorsList="aurhorsList" />
      </div>
      <div class="row justify-content-center">
        <SingleCard class="col-2 me-3" v-for="(element, index) in filteredCards" :key="index" :index='index'
          :element="element" />
      </div>
    </div>
    <LoaderApp v-if="(!loader)" />
  </main>
</template>

<script>
import SingleCard from './singleCard.vue'
import LoaderApp from './loaderApp.vue'
import genresUser from './genresUser.vue'
import authorsUser from './authorsUser.vue'
import axios from 'axios'

export default {
  components: {
    SingleCard,
    LoaderApp,
    genresUser,
    authorsUser,
  },
  data: function () {
    return {
      cardsList: [],
      filteredCards: [],
      loader: false,
      userSelected: '',
      authorSelected: '',
      genresList: [],
      authorsList: [],
    }
  },
  methods: {
    getCard() {
      axios.get('https://flynn.boolean.careers/exercises/api/array/music')
        .then((result) => {
          this.cardsList = result.data.response
          this.filteredCards = [...this.cardsList]
          this.initGenres()
          this.initAuthors()
          this.timeOut()
          this.searchGenre(this.userSelected)
          this.searchAuthor(this.authorSelected)

        })
    },
    timeOut() {
      setTimeout(() => {
        this.loader = true
      }, 2000)
    },
    searchGenre(element) {
      console.log(element)
      this.filteredCards = [...this.cardsList].filter((artist) => artist.genre.includes(element))
    },
    searchAuthor(element) {
      this.filteredCards = [...this.cardsList].filter((artist) => artist.author.includes(element))
    },
    setUserSelect(choice) {
      this.userSelected = choice
      this.searchGenre(this.userSelected)
    },
    initGenres() {
      for (let i = 0; i < this.cardsList.length; i++) {
        if (!this.genresList.includes(this.cardsList[i].genre)) {
          this.genresList.push(this.cardsList[i].genre)
        }
      }
    },
    initAuthors() {
      for (let i = 0; i < this.cardsList.length; i++) {
        if (!this.authorsList.includes(this.cardsList[i].author)) {
          this.authorsList.push(this.cardsList[i].author)
        }
      }
    },
    created() {
      this.getCard()
    },
  }
}
</script>

<style scoped lang="scss">
@import "../assets/style/variables.scss";

main {
  height: calc(100vh - 70px);
  background-color: $backgroundMain;
}
</style>
