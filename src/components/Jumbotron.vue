<template>
  <div id="jumbo">

  </div>
</template>

<script>
export default {
  name : 'Jumbotron'

}
</script>

<style lang="scss">
  #jumbo{
    background-image: url('../assets/img/jumbo.jpg');
    background-position: center;
    background-size: cover;
    height: calc(100vh - 100px);
    margin-top: 100px
  }
</style>