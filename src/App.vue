<template>
  <div id="app">
    <img src="./assets/Pokemon_logo.svg" alt="logo Pokémon" />
    <form-search @getPokemon="getPokemon" />
    <template>
      <info-pokemon
        v-if="datosPokemon"
        :img="img"
        :abilities="abilities"
        :moves="moves"
      />
      <h3 v-else v-text="connectionApi" />
    </template>
  </div>
</template>

<script>
import FormSearch from "@/components/FormSearch.vue";
import InfoPokemon from "@/components/InfoPokemon.vue";

export default {
  name: "App",
  components: {
    InfoPokemon,
    FormSearch,
  },
  data() {
    return {
      datosPokemon: null,
      stateSearch: true,
    };
  },
  computed: {
    abilities() {
      return this.datosPokemon.abilities
        // .slice(0, 10) // diez primeras habilidades
        .map((item) => this.parseText(item.ability.name));
    },
    moves() {
      return this.datosPokemon.moves
        // .slice(0, 10) // diez primeros movimientos
        .map((item) => this.parseText(item.move.name));
    },
    img() {
      return this.datosPokemon.sprites.front_default;
    },
    connectionApi() {
      return this.stateSearch ? "Loading..." : "Pokémon no encontrado";
    },
  },
  methods: {
    async getPokemon(nombre) {
      this.stateSearch = true;
      this.datosPokemon = null;
      try {
        const response = await fetch(
          `https://pokeapi.co/api/v2/pokemon/${nombre}`
        );
        if (!response.ok) throw "Error en API";
        this.datosPokemon = await response.json();
      } catch (error) {
        console.log(error);
        this.stateSearch = false;
      }
    },
    parseText(text) {
      return text.replace(/^.|-/g, (s) => (s == "-" ? " " : s.toUpperCase()));
    },
  },
  beforeCreate() {
    document.title = "PokeGuía";
  },
  created() {
    this.getPokemon("pikachu");
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
