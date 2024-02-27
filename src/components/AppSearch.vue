<template>
  <div class="search-area">
    <!-- input and button for search -->
    <div class="search-group">
      <input 
        placeholder="Search the pokemon" 
        class="search-input" 
        type="text" 
        @keyup.enter="fetch"
        v-model="searchedPokemon"
      >
      <button class="search-submit" @click="fetch">Search</button>
    </div>
    
    <button v-if="!(alreadyInMyPokedex)" @click="catchIt" class="catch">Catch it !</button>
    <button @click="removeIt" v-else class="remove">Rimuovi</button>
  </div>
</template>

<script>

  export default {
    data() {
      return {
        searchedPokemon: null
      }
    },

    props: {
      alreadyInMyPokedex: Boolean
    },

    methods: {
      fetch() {
        this.$emit('getPokemon', this.searchedPokemon);
        this.searchedPokemon = null;
      },

      catchIt() {
        this.$emit('catchPokemon');
      },

      removeIt() {
        this.$emit('removePokemon');
      }
    }
  }
</script>

<style lang="scss" scoped>
@use '../styles/partials/vars' as *;
.search-area {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  padding: 0 14px;
  .search-group {
    display: flex;
    gap: 10px;
    margin-bottom: 5px;
    .search-input {
      line-height: 32px;
      padding: 0 7px;
      border: 3px solid $pokeDarkRed;
      background-color: $grey;

      &:focus {
        border-color: $pokeBlue;
      }
    }

    .search-submit {
      line-height: 32px;
      padding: 0 10px;
      border-radius: 10px;
      color: $white;
      background-color: $pokeBlue;
      cursor: pointer;
      transition: all 100ms ease-in;

      &:hover {
        background-color: $pokeLightBlue;
      }

      &:active {
        transform: scale(0.8);
      }
    }
  }

  .catch, .remove {
    background-color: $pokeCelestial;
    color: $white;
    padding: 0 10px;
    line-height: 34px;
    border-radius: 20% 0 20% 0;
    cursor: pointer;

    &:hover {
      background-color: $pokeDarkCelestial;
    }
  }
}

</style>