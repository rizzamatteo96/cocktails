<template>
  <div class="container">
    <!-- titolo della sezione -->
    <h2 class="sec-title txt-center">Questo è il tuo cocktail casuale:</h2>

    <!-- inizio conenuto sezione -->
    <div class="sec-content row jc-space-between ai-center mt-1">
      <!-- inizio sezione testo drink -->
      <div class="col-xs-12 col-md-6 drink-text">

        <!-- nome del cocktail -->
        <h3>{{random.strDrink}}</h3>

        <!-- inizio sezione ingredienti -->
        <p><span class="underline">Ingredienti</span> :  
          <ul class="ingredients">
            <li
            v-for="(element,k) in ingredients" :key="k"
            class="light-bk">{{element}}</li>
          </ul>
        </p>
        <!-- fine sezione ingredienti -->

        <!-- inizio sezione IBA -->
        <p v-if="random.strIBA">
          <span class="underline">Commento da 
            <a class="txt-black" target="_blank" href="https://it.wikipedia.org/wiki/International_Bartenders_Association">IBA</a>
          </span> : 
          <span class="light-bk">{{random.strIBA}}</span>
        </p>
        <!-- fine sezione IBA -->

        <!-- inizio pulsante video ricetta -->
        <a 
        v-if="random.strVideo"
        class="video mt-1"
        :href="random.strVideo" 
        target="_blank">
          <i class="fab fa-youtube"></i>
          <span class="txt-yt">Guarda il video della ricetta</span> 
        </a>
        <!-- fine pulsante video ricetta -->
      </div>
      <!-- fine sezione testo drink -->

      <!-- inizio sezione foto drink -->
      <img :src="random.strDrinkThumb" alt="test img" class="col-xs-12 col-md-6 h-100">
      <!-- fine sezione foto drink -->
    </div>
    <!-- fine contenuto sezione -->

    <!-- inizio footer sezione -->
    <div class="sec-footer">
      <button @click="callRandom" class="reload-rand">
        <i class="fas fa-sync-alt"></i>
        <span class="txt-rel">Calrica un altro cocktail</span> 
      </button>
    </div>
    <!-- fine footer sezione -->

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
      ingredients: [],
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
        })
        .finally(() => {
          // resetta la lista degli ingredienti
          this.ingredients = [];
          // estrapola dall'oggetto che arriva dall'array la lista di ingredienti e li salva da parte 
          // se presenti per la visualizzazione
          for(var key in this.random){
            if(key.includes('strIngredient') && this.random[key]){
              // console.log(key + '  ' + this.random[key]);
              this.ingredients.push(this.random[key]);
              console.log(this.ingredients);
            }
          }
        })
    }
  },
  created(){
    this.callRandom();
  }
}
</script>

<style lang="scss">
  .sec-title,
  .sec-footer{
    height: 100px;
  }

  .sec-content{
    h2{
      font-size: 3rem;
    }
  
    .drink-text{
      
      & > *{
        margin: 1rem 0;
      }
  
      h3{
        font-size: 2rem;
        margin-bottom: 3rem;
      }
      
      .light-bk{
        color: #555;
      }
    
      .ingredients{
        margin-left: 1rem;
        display: inline-block;
        vertical-align: text-top;
  
        li::marker{
          color: black;
          font-size: 10px;
        }
      }
    
      .video{
        display: inline-block;
        margin-top: 3rem;
        padding: 1rem 2rem;
        border-radius: 50px;
        border: 2px solid black;
        background-color: black;
        overflow: hidden;
        cursor: pointer;
        text-decoration: none;
        color: white;
        position: relative;
        white-space: nowrap;
        animation-name: chiudiPulsante;
        animation-duration: .2s;
  
        &:hover{
          animation-name: apriPulsante;
          animation-duration: .5s;
          animation-fill-mode: forwards;
          
          .txt-yt{
            display: inline;
          }
        }
  
        .txt-yt{
          display: none;
          overflow: hidden;
          margin-left: 2rem;
        }
      }
    }
  
    img{
      height: 100%;
      filter: grayscale(100%);
      transition: filter .5s;
  
      &:hover{
        filter: grayscale(0%);
      }
    }
  }

  .sec-footer{
    text-align: center;

    .reload-rand{
    display: inline-block;
    margin-top: 3rem;
    padding: 1rem 2rem;
    border-radius: 50px;
    border: 2px solid black;
    background-color: black;
    overflow: hidden;
    cursor: pointer;
    text-decoration: none;
    color: white;
    position: relative;
    white-space: nowrap;
    animation-name: chiudiPulsanteRel;
    animation-duration: .2s;

      &:hover{
        animation-name: apriPulsanteRel;
        animation-duration: .5s;
        animation-fill-mode: forwards;
        
        .txt-rel{
          display: inline;
        }
      }

      .txt-rel{
        display: none;
        overflow: hidden;
        margin-left: 2rem;
      }
    }

  }

  @keyframes apriPulsante {
    from{
      width: 18%;
      background-color: black;
      color: white;
    }
    to{
      width: 62%;
      background-color: white;
        color: black;
    }
  }

  @keyframes chiudiPulsante {
    from{
      width: 62%;
      background-color: white;
        color: black;
    }
    to{
      width: 18%;
      background-color: black;
      color: white;
    }
  }

  @keyframes apriPulsanteRel {
    from{
      width: 9%;
      background-color: black;
      color: white;
    }
    to{
      width: 30%;
      background-color: white;
        color: black;
    }
  }

  @keyframes chiudiPulsanteRel {
    from{
      width: 30%;
      background-color: white;
      color: black;
    }
    to{
      width: 9%;
      background-color: black;
      color: white;
    }
  }
  
</style>