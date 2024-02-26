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
    
  </div>
</template>

<script>

  export default {
    data() {
      return {
        searchedPokemon: null
      }
    },

    methods: {
      fetch() {
        this.$emit('getPokemon', this.searchedPokemon);
        this.searchedPokemon = null;
      }
    }
  }
</script>

<style lang="scss" scoped>
@use '../styles/partials/vars' as *;
.search-area {

  .search-group {
    display: flex;
    gap: 10px;

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
}

</style>