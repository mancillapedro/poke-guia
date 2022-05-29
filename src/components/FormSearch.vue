<template>
  <form @submit.prevent="getPokemon">
    <legend><h1>PokeGuía</h1></legend>
    <label for="input">Nombre</label>
    <input
      id="input"
      type="text"
      placeholder="Ingrese Pokémon"
      v-model="input"
      required
    />
    <button type="submit">Buscar</button>
  </form>
</template>

<script>
export default {
  name: "FormSearch",
  data() {
    return {
      input: "",
    };
  },
  methods: {
    getPokemon() {
      this.$emit("getPokemon", this.input);
      this.input = "";
    },
  },
};
</script>

<style scoped>
form > * {
  margin: 0 0.2rem;
}
</style>