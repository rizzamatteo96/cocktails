<template>
  <div class="container">
    <h2>Questo è il tuo cocktail casuale:</h2>
    <div class="row jc-space-between mt-1">
      <div class="col-xs-12 col-md-6">
        <h3><span class="underline">Nome</span> :  <span class="light-bk">{{random.strDrink}}</span> </h3>
        <button v-if="random.strVideo" class="video">
          <a :href="random.strVideo" target="_blank">Guarda il video della ricetta</a>
        </button>
      </div>
      <div class="col-xs-12 col-md-6">
        <img :src="random.strDrinkThumb" alt="test img">
      </div>
    </div>

  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Randoms',
  data(){
    return{
      urlApi: 'https://www.thecocktaildb.com/api/json/v1/1/random.php',
      random: {},

    }
  },
  methods: {
    callRandom(){
      axios
        .get(this.urlApi)
        .then((response) => {
          console.log(response.data.drinks[0]);
          this.random = response.data.drinks[0];
        })
        .catch((e) => {
          console.log(e);
        });
    }
  },
  created(){
    this.callRandom();
  }
}
</script>

<style lang="scss">
  .light-bk{
    color: #555;
  }

  .video{
    padding: 10px 25px;
    border: none;
    border-radius: 50px;
    background-color: black;
    cursor: pointer;

    &:hover{
      border: 2px solid black;
      background-color: #fff;
      a{
        color: black;
      }
    }

    a{
      text-decoration: none;
      color: white;
    }
  }

  img{
    filter: grayscale(100%);
    transition: filter .5s;

    &:hover{
      filter: grayscale(0%);
    }
  }
</style>