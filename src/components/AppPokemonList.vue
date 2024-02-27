<script>
  export default {
    props: {
      pokedex: Array
    },

    methods: {
      getDetails(pokemonName) {
        this.$emit('getPokemonDetails', pokemonName);
      }
    }
  }
</script>


<template>
  <div class="my-pokemons">
    <h3>My pokemons</h3>
    <ul class="pokemons" v-if="pokedex.length !== 0">
      <li 
      class="current-pokemon"
      @click="getDetails(poke.name)" v-for="(poke, i) in pokedex" :key="poke.id">
        {{ poke.name }}
      </li>
    </ul>
    <span v-else>Nessun pokemon presente</span>
  </div>
</template>


<style lang="scss" scoped>
@use '../styles/partials/vars' as *;
.my-pokemons {
  background-color: $pokeGrey;
  color: $white;
  padding: 20px;
  border-radius: 10px;
  max-width: 340px;
  margin: 0 auto;
  max-height: 300px;
  overflow: auto;

  h3 {
    margin-bottom: 24px;
  }

  .pokemons {
    .current-pokemon {
      cursor: pointer;
      margin-bottom: 10px;
    }
  }
}

</style>