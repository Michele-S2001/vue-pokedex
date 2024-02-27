<template>
  <div class="pokemon-details">
    <div class="pokemon-details__header">
      <img v-if="!(pokemon)" src="../../img/pokeball.png" alt="pokeball placeholder">
      <img v-else :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${pokemon.id}.png`">
    </div>

    <div class="pokemon-details__body">

      <div v-if="!(pokemon)" class="none-pokemon">
        <p>No pokemon searched or matched</p>
      </div>

      <div v-else class="details-inner">

        <!-- generic properties -->
        <div class="pokeDetail"><strong>Name:</strong> {{ pokemon.name }}</div>
        <div class="pokeDetail">
          <strong>Type: </strong> 
          <div class="types-outer">
            <span class="type" v-for="(pokeTypes, i) in pokemon.types" :key="i">
              <span>{{ pokeTypes.type.name }}</span>
            </span>
          </div>
        </div>
        <div class="pokeDetail"><strong>Height:</strong> {{ pokemon.height }}''</div>
        <div class="pokeDetail"><strong>Weight:</strong> {{ pokemon.weight }}</div>
        <!-- end generic properties -->

        <!-- Stats -->
        <div class="stats">
          <h4>Stats</h4>
          <div class="stats__inner">
            <div class="stat" v-for="(currStat, i) in pokemon.stats" :key="i">
              <strong>{{ currStat.stat.name }}</strong><span>{{ currStat.base_stat }}</span>
            </div>
          </div>
        </div>
      </div>

    </div>
  </div>
</template>

<script>
  export default {
    props: ['pokemon']
  }
</script>

<style lang="scss" scoped>
@use '../styles/partials/vars' as *;
.pokemon-details {
  margin-top: 24px;

  &__header {
    img {
      clip-path: polygon(50% 0%, 100% 0, 100% 100%, 75% 100%, 10% 100%, 0 90%, 0 0);
      border-radius: 8px;
      width: 230px;
      height: 180px;
      object-fit: cover;
      border: 16px solid $grey;
      margin: 0 auto;
      background-color: $white;
    }
    margin-bottom: 18px;
  }

  &__body {
    .none-pokemon {
      color: $white;
      text-align: center;
    }

    .details-inner {
      background-color: $pokeGreen;
      border-radius: 8px;
      box-shadow: -1px 1px 0px 1px $black;
      padding: 10px;

      .pokeDetail > .types-outer {
        display: inline-block;

        & > *:not(:last-child)::after {
          content: '-';
          display: inline-block;
          width: 10px;
          text-align: center;
        }
      }

      .stats {
        margin-top: 18px;

        h4 {
          margin-bottom: 5px;
          border-bottom: 1px solid $black;
        }

        &__inner {
          .stat {
            display: flex;

            span {
              margin-left: auto;
            }
          }
        }
      }
    }
  }
}
</style>