<template>
  <section class="randomCocktail">
    <Randoms/>
  </section>
</template>

<script>
import Randoms from './componentsMain/Randoms.vue'

export default {
  name : 'Main',
  components : {
    Randoms

  }
}
</script>

<style lang="scss">
  section{
    margin: 5rem 0;
  }
</style>