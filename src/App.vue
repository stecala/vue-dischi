<template>
  <div id="app">
    <HeaderApp />
    <MainApp />
    <FooterApp />
  </div>
</template>

<script>
import MainApp from './components/mainApp.vue'
import HeaderApp from './components/headerApp.vue'
import FooterApp from './components/footerApp.vue'

export default {
  name: 'App',
  components: {
    MainApp,
    HeaderApp,
    FooterApp,
  }
}

</script>

<style lang="scss">
@import "~bootstrap/scss/bootstrap";

</style>
