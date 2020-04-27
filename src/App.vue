<template>
  <div id="app">
    <h1 class="title">Consultar Datos</h1>
    <button v-on:click="fetch">Consultar</button>
    <div v-for="character in characters" v-bind:key="character.id">
      {{ character }}
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      characters: [],
    };
  },
  methods: {
    fetch() {
      let result = this.$http
        .get("https://rickandmortyapi.com/api/character")
        .then((res) => {
          this.characters = res.data.results;
          console.log(res.data);
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
};
</script>
