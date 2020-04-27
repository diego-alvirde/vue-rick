<template>
  <div id="app">
    <div class="hero is-white is-gradient is-bold">
      <div class="hero-body">
        <h1 class="title">
          <span class="has-text-success">R&M</span>
          <span class="subtitle">Personajes</span>
        </h1>
        <button v-on:click="fetch" class="button is-success is-rounded">
          Consultar
        </button>
      </div>
    </div>
    <div class="container">
      <div
        class="columns is-desktop is-mobile is-tablet is-multiline is centered"
      >
        <Character
          v-for="character in characters"
          :key="character.id"
          :character="character"
        />
      </div>
    </div>
  </div>
</template>

<script>
import Character from "./components/Character";
export default {
  name: "App",
  components: {
    Character,
  },
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
  created() {
    this.fetch();
  },
};
</script>
