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
        <div
          class="column is-12-mobile is-4-desktop is-4-tablet"
          v-for="character in characters"
          v-bind:key="character.id"
        >
          <div class="card">
            <div class="card-header">
              <img :src="character.image" :alt="character.name" />
            </div>
            <div class="card-content">
              <h3 class="title is-size-4">{{ character.name }}</h3>
              <button class="button is-success is-rounded is-small">
                Ver mas
              </button>
            </div>
          </div>
        </div>
      </div>
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
