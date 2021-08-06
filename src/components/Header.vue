<template>
  <div class="title">
    <div class="container h-100">
      <div class="row jc-start ai-center">
        <img class="h-100" src="../assets/img/logo.png" alt="">
        <h1>RizTails</h1>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name : 'Header'
}
</script>

<style lang="scss">
  .title{
    position: fixed;
    z-index: 9999;
    top: 0;
    left: 0;
    right: 0;
    background-color: #ddddddcc;
    height: 100px;


    .container{
      padding: 1rem 0;

      img{
        margin-right: 1rem;
        border-radius: 50%;
        border: 3px solid black
      };
    }
  }
</style>