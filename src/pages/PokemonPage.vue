<template>
<h1 v-if="!pokemon">Espere por favor...</h1>
<div v-else>
   <h1>¿Quién es este pokémon?</h1>
<pokemon-picture :pokemonId="pokemon.id" :showPokemon="showPokemon"></pokemon-picture>
 <pokemon-options :pokemons="pokemonArr" @selection="checkAnswer"></pokemon-options>

   <div v-if="showAnswer">
      <h2 class="fade-in">{{message}}</h2>
      <button @click="newGame" >Nuevo Juego</button>
   </div>
</div>

 
</template>

<script>
import PokemonOptions from '../components/PokemonOptions.vue'
import PokemonPicture from '../components/PokemonPicture.vue'
import getPokemonOptions from '@/helpers/getPokemonOptions'
//console.log(getPokemonOptions())

export default {
  components: { PokemonOptions, PokemonPicture },
  data(){
    return{
      pokemonArr:[],
      pokemon: null,
      showPokemon: false,
      showAnswer:false,
      message:''
    }
  },
  methods:{
    async mixpokemonArray(){
      this.pokemonArr = await getPokemonOptions()
       const rndInt = Math.floor(Math.random() * 4 )
       this.pokemon = this.pokemonArr[rndInt]
    },
    checkAnswer(  selectedId){
      this.showPokemon=true
      this.showAnswer =true
       if(selectedId === this.pokemon.id){
         this.message = `Correcto, ${ this.pokemon.name }`
       }
       else{
         this.message = `Oops, era ${ this.pokemon.name }`
       }
      /* console.log('PokemonPage', pokemonId) */
    },
    newGame(){
      this.showPokemon =false
      this.showAnswer =false
      this.pokemonArr = []
      this.pokemon = null
      this.mixpokemonArray()
    }
  },
  mounted(){
    this.mixpokemonArray()
  }
}
</script>
