<template>
  <header class="page-header">
    <div class="container">
      <img class="poke-logo" src="../../img/Pokédex_logo.png" alt="pokedex logo">
    </div>
  </header>
</template>

<style lang="scss" scoped>
@use '../styles/partials/vars' as *;
.page-header {
  padding: 20px 10px;
  box-shadow: 0px 4px 10px 1px rgba($pokeBlue, $alpha: 0.7);
  .poke-logo {
    margin: 0 auto;
    width: 240px;
  }
}

</style>