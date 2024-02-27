<script>
import AppSearch from './AppSearch.vue';
import AppPokemonDetails from './AppPokemonDetails.vue';
import AppPokemonList from './AppPokemonList.vue';
import axios from 'axios';

export default {
  components: {
    AppSearch,
    AppPokemonList,
    AppPokemonDetails
  },

  data() {
    return {
      pokemonSearchResult: null,
      myPokedex: [],
      inPokedex: false
    }
  },

  methods: {
    fetchPokemon(pokemonSearchResult) {
      if(pokemonSearchResult) {
        const toLowerCaseName = pokemonSearchResult.toLowerCase()
        // Get the pokemon
        axios
          .get(`https://pokeapi.co/api/v2/pokemon/${toLowerCaseName}`)
          .then((res) => {
            this.pokemonSearchResult = res.data;
            this.isInPokedex();
          })
      }
      // delete v-model value once the searching process is done
      this.pokemonSearchResult = null;
      this.inPokedex = false;
    },

    addToPokedex() {
      if(this.pokemonSearchResult) {
        //aggiungo il pokemon all'array
        this.myPokedex.push({
          id: this.pokemonSearchResult.id,
          name: this.pokemonSearchResult.name
        });
        //sovrascrivo l'array
        this.savePokedex();
        this.isInPokedex();
      }
    },

    deleteToPokedex() {
      this.myPokedex = this.myPokedex.filter((el) => el.id !== this.pokemonSearchResult.id);
      this.savePokedex();
      this.isInPokedex();
    },

    recoverPokedex() {
      const storagedPokedex = localStorage.getItem('personalPokedex');
      if(storagedPokedex) {
        this.myPokedex = JSON.parse(storagedPokedex);
      }
    },

    savePokedex() {
      localStorage.setItem('personalPokedex', JSON.stringify(this.myPokedex));
    },

    isInPokedex() {
      //check if it's in my pokedex
      if (this.myPokedex.some((el) => el.id === this.pokemonSearchResult.id)) {
        this.inPokedex = true
      } else {
        this.inPokedex = false
      }
    },

    getDetails(pokeName) {
      this.fetchPokemon(pokeName);
    }
  },

  mounted() {
    this.recoverPokedex();
  }
}
</script>


<template>
  <section class="main-content">
    <div class="container">
      <div class="pokedex">
        <!-- details and search section -->
        <div class="pokedex__search-details">
          <AppSearch 
            @getPokemon="fetchPokemon" @catchPokemon="addToPokedex"
            @removePokemon="deleteToPokedex" 
            :searchResult="pokemonSearchResult"
            :alreadyInMyPokedex="inPokedex"/>
          <AppPokemonDetails :pokemon="pokemonSearchResult"/>
        </div>
        <!-- end of details and search section -->

        <!-- my pokemons section -->
        <div class="pokedex__pokemons">
          <AppPokemonList 
          @getPokemonDetails="getDetails"
          :pokedex="myPokedex"/>
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
  padding-bottom: 40px;
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
      padding: 20px;
    }
    
  }
}

@media (max-width: 980px) {
  .main-content {
    .pokedex {
      grid-template-columns: 1fr;
    }
  }
}

</style>