<template>
  <main class="d-flex justify-content-center align-items-center">
    <div class="container pt-5" v-if="(loader)">
      <div class="row">
        <genresUser class="col-4 m-auto" @select="setUserSelect" :genresList="genresList"  />
        <authorsUser class="col-4 m-auto" @selectAuthor="setAuthorSelect" :authorsList="filteredAuthors" v-if="(genreSelected!='')"  />
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
      loader: false,
      genreSelected: '',
      authorSelected: '',

      filteredCards: [],
      genresList: [],
      authorsList: [],
      filteredAuthors: [],
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
          this.searchGenre(this.genreSelected)
          this.searchAuthor(this.authorSelected)

        })
    },
    timeOut() {
      setTimeout(() => {
        this.loader = true
      }, 2000)
    },

    // genres zone
    searchGenre(element) {
      this.filteredCards = this.cardsList.filter((artist) => artist.genre.includes(element))

    },
    setUserSelect(choice) {
      this.genreSelected = choice
      this.searchGenre(this.genreSelected)
      this.onGenreSelected(this.genreSelected)
    },
    initGenres() {
      for (let i = 0; i < this.cardsList.length; i++) {
        if (!this.genresList.includes(this.cardsList[i].genre)) {
          this.genresList.push(this.cardsList[i].genre)
        }
      }
    },


    // author zone
    searchAuthor(element) {
      this.filteredCards = this.cardsList.filter((artist) => artist.author.includes(element))
    },

    setAuthorSelect(choice) {
      this.authorSelected = choice
      this.searchAuthor(this.authorSelected)
    
    },

    initAuthors() {
      for (let i = 0; i < this.cardsList.length; i++) {
        if (!this.authorsList.includes(this.cardsList[i].author)) {
          this.authorsList.push(this.cardsList[i].author)
        }
      }
    },
    onGenreSelected(selectedGenre){
        this.filteredAuthors = this.filteredCards.filter((card)=> card.genre == selectedGenre).map((card) => card.author)
    }

  },

  created() {
    this.getCard()
  },
}
</script>

<style scoped lang="scss">
@import "../assets/style/variables.scss";

main {
  height: calc(100vh - 70px);
  background-color: $backgroundMain;
}
</style>
