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
  <PokemonSearch @pokemon-found="showPokemon" />

  <PokemonDetails v-if="selectedPokemon" :pokemon="selectedPokemon" @catch-pokemon="updatePokemonList"
    @release-pokemon="updatePokemonList" />

  <Pokedex :pokemon-list="pokemonList" @pokemon-selected="showPokemonDetails" />

</template>

<style lang="scss"></style>
