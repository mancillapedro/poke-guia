<template>
  <article v-if="img">
    <img :src="img" alt="" />
    <section>
      <h2>Movimientos</h2>
      <ul>
        <li v-for="(move, i) in moves" :key="i" v-text="move" />
      </ul>
    </section>
    <section>
      <h2>Habilidades</h2>
      <ul>
        <li v-for="(habilidad, i) in abilities" :key="i" v-text="habilidad" />
      </ul>
    </section>
  </article>
</template>

<script>
export default {
  name: "InfoPokemon",
  props: {
    img: {
      type: String,
      required: true,
      default() {
        return "";
      },
    },
    moves: {
      type: Array,
      required: true,
      default() {
        return [];
      },
    },
    abilities: {
      type: Array,
      required: true,
      default() {
        return [];
      },
    },
  },
};
</script>

<style scoped>
ul {
  padding: 0;
}
li {
  list-style: none;
}
</style>
