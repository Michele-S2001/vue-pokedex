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
    <ul class="pokemon" v-if="pokedex.length !== 0">
      <li @click="getDetails(poke.name)" v-for="(poke, i) in pokedex" :key="i">
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

  h3 {
    margin-bottom: 24px;
  }
}

</style>