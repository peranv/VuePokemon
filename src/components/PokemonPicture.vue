<template>
 <div class="pokemon-container">
 <img v-if="!showPokemon" 
        :src="imgSrc" 
  alt="pokemon"
  class="hidden-pokemon">
  <img v-else:="showPokemon" 
          :src="imgSrc" 
  alt="pokemon"
  clase="fade-in">
 </div>
 
</template>

<script>
export default {
    props:{
        pokemonId:{
            type: Number,
            requiered:true
        },
        showPokemon:{
            type:Boolean,
            requiered: true,
            default: false
        }
    },
   computed:{
       imgSrc(){
         return `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${this.pokemonId}.svg`
       }
   }
}
</script>

<style scoped>
 /* Pokemon Picture */
.pokemon-container {
    height: 200px;
}
img {
    height: 200px;
   /*  position: absolute;
    right: 32%; */
    user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    -webkit-user-drag: none;
    -webkit-user-select: none;
}
.hidden-pokemon {
    filter: brightness(0);
}

</style>