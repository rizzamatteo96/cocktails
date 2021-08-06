<template>
  <div id="app">
    <Header/>
    <Jumbotron/>
    <Main/>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Jumbotron from './components/Jumbotron.vue'
import Main from './components/Main.vue'

export default {
  name: 'App',
  components: {
    Header,
    Jumbotron,
    Main
  }
}
</script>

<style lang="scss">
@import '@/style/commons.scss'
</style>
