<template>
  <div id="app">
    <div class="hero is-white is-gradient is-bold">
      <div class="hero-body">
        <h1 class="title">
          <span class="has-text-success">Propiedad </span>
          <span class="subtitle">horizontal</span>
        </h1>

        <div class="field has-addons is-pulled-right">
          <div class="control">
            <input
              v-model="search"
              type="text"
              class="input is-rounded"
              v-on:keyup.enter="searchData"
            />
          </div>

          <div class="control">
            <button
              v-on:click="searchData"
              class="button is-success is-rounded"
            >
              Buscar
            </button>
          </div>
        </div>
      </div>
    </div>

    <div class="table-container">
      <div class="table">
        <thead>
          <tr>
            <th>Nombre</th>
            <th>Estado</th>
            <th>Especie</th>
            <th>Genero</th>
          </tr>
        </thead>
        <tbody>
          <character
            v-for="character of characters"
            v-bind:key="character.id"
            v-bind:character="character"
          />
        </tbody>
      </div>
      <nav class="pagination" role="navigation" aria-label="pagination">
        <a class="pagination-previous" v-on:click="changePage(page - 1)"
          >Anterior</a
        >

        <ul class="pagination list">
          <a class="pagination-link is-current">{{ page }}</a>
        </ul>

        <a class="pagination-previous" v-on:click="changePage(page + 1)"
          >Siguiente</a
        >
      </nav>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Character from "./components/Character";

export default {
  name: "App",
  components: {
    Character,
  },
  data: function () {
    return {
      characters: [],
      page: 1,
      pages: 1,
      search: " ",
    };
  },
  created() {
    this.clickBoton();
  },
  methods: {
    clickBoton() {
      const params = {
        page: this.page,
        name: this.search,
      };
      let result = axios
        .get("https://rickandmortyapi.com/api/character", { params })
        .then((res) => {
          this.characters = res.data.results;
          this.pages = res.data.info.pages;
          console.log(res.data);
        })
        .catch((err) => {
          console.log(err);
        });
    },
    changePage(page) {
      this.page = page <= 0 || page >= this.pages ? this.page : page;
      this.clickBoton();
    },
    searchData() {
      this.page = 1;
      this.clickBoton();
    },
  },
};
</script>

