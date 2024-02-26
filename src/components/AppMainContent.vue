<script>
import AppSearch from './AppSearch.vue';
import axios from 'axios';

export default {
  components: {
    AppSearch
  },

  data() {
    return {
      searchedPokemon: null
    }
  },

  methods: {
    fetchPokemon(searchedPokemon) {
      console.log(searchedPokemon);

      // Get the pokemon
      axios
        .get(`https://pokeapi.co/api/v2/pokemon/${searchedPokemon}`)
        .then((res) => {
          this.searchedPokemon = res.data;
        })

      // delete v-model value once the searching process is done
      this.searchedPokemon = '';
    }
  }
}
</script>


<template>
  <section class="main-content">
    <div class="container">
      <div class="pokedex">
        <!-- details and search section -->
        <div class="pokedex__search-details">
          <AppSearch @getPokemon="fetchPokemon"/>
        </div>
        <!-- end of details and search section -->

        <!-- my pokemons section -->
        <div class="pokedex__pokemons">

        </div>
        <!-- end of my pokemons section -->
      </div>
    </div>
  </section>
</template>


<style lang="scss" scoped>
@use '../styles/partials/vars' as *;
.main-content {
  padding-top: 70px;
  padding-left: 15px;
  padding-right: 15px;

  .pokedex {
    background-color: $pokeRed;
    border-radius: 20px;
    min-height: 300px;
    display: grid;
    grid-template-columns: repeat(2, 1fr);

    &__search-details {
      //end debug properties
      padding: 15px 20px;
      border-right: 2px solid $pokeDarkRed;
    }

    
    &__pokemons {
      border-left: 2px solid $pokeDarkRed;
    }
    
  }
}

</style>