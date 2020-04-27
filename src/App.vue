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
      <nav class="pagination" role="navegation" aria-label="pagination">
        <a class="pagination-previous" v-on:click="changePage(page - 1)"
          >Anterior</a
        >

        <ul class="pagination-list">
          <li>
            <a class="pagination-link is-current">{{ page }}</a>
          </li>
        </ul>

        <a class="pagination-next" v-on:click="changePage(page + 1)"
          >Siguiente</a
        >
      </nav>
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
      page: 1,
      pages: 1,
    };
  },
  methods: {
    fetch() {
      const params = {
        page: this.page,
      };

      let result = this.$http
        .get("https://rickandmortyapi.com/api/character", { params })
        .then((res) => {
          this.characters = res.data.results;
          this.pages = res.data.info.pages;
        })
        .catch((error) => {
          console.log(error);
        });
    },
    changePage(page) {
      this.page = page <= 0 || page > this.pages ? this.page : page;
      this.fetch();
    },
  },
  created() {
    this.fetch();
  },
};
</script>
