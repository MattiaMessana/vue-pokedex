<script>
import PokemonSearch from './components/PokemonSearch.vue';
import PokemonDetails from './components/PokemonDetails.vue';
import Pokedex from './components/Pokedex.vue';


export default {
  components: {
    PokemonSearch,
    PokemonDetails,
    Pokedex,
  },
  data() {
    return {
      selectedPokemon: null,
      pokemonList: [],
    };
  },
  methods: {
    showPokemon(pokemon) {
      this.selectedPokemon = pokemon;
    },
    showPokemonDetails(pokemon) {
      this.selectedPokemon = pokemon;
    },
    updatePokemonList() {
      this.pokemonList = Object.keys(localStorage).map(key => JSON.parse(localStorage.getItem(key)));
    },
  },
  mounted() {
    this.updatePokemonList();
  }
};
</script>

<template>

  <div class="container bg rounded-4 mt-5 text-center">
    <div class="row">
      <div class="col">
        <PokemonSearch @pokemon-found="showPokemon" />

        <PokemonDetails v-if="selectedPokemon" :pokemon="selectedPokemon" @catch-pokemon="updatePokemonList"
          @release-pokemon="updatePokemonList" />
      </div>

      <div class="col">
        <Pokedex :pokemon-list="pokemonList" @pokemon-selected="showPokemonDetails" />
      </div>

    </div>
  </div>

</template>

<style lang="scss">
  .bg {
    background-color: red;
    width: 100vw;
    // debug
    height: 500px;
  }

  p {
    color: white;
  }
</style>
