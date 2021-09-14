<template>
  <div id="app">
    <header>
      <div class="container">
        <img class="logo" src="@/assets/images/Boolflix_logo.png" alt="" />
        <Search @search="getResults" />
      </div>
    </header>
    <main>
      <div class="container">
        <Results title="Film" id="film" :items="movies" />
        <Results title="Serie TV" id="series" :items="series" />
      </div>
    </main>
  </div>
</template>

<script>
import axios from "axios";

import Search from "@/components/Search.vue";
import Results from "@/components/Results.vue";

export default {
  name: "App",
  components: {
    Search,
    Results,
  },
  data() {
    return {
      movies: [],
      series: [],
      api: {
        key: "cfc0856a6e486ed1f7367bd371b61e4e",
        baseUri: "https://api.themoviedb.org/3",
      },
    };
  },
  methods: {
    getResults(query) {
      if (!query) {
        this.movies = this.series = [];
        return;
      }
      this.fetchApi(query, "search/movie", "movies");
      this.fetchApi(query, "search/tv", "series");
    },
    fetchApi(query, endPoint, entity) {
      const params = {
        params: {
          query,
          api_key: this.api.key,
          language: "it_IT",
        },
      };
      axios.get(`${this.api.baseUri}/${endPoint}`, params).then((res) => {
        this[entity] = res.data.results;
      });
    },
  },
};
</script>

<style lang="scss">
/* Generals */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html,
body {
  width: 100vw;
  height: 100vh;
  overflow-x: hidden;
  background-color: #111010;
  font-family: sans-serif,Helvetica, Arial;
  color: white;
}

.container {
  height: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

ul {
  list-style-type: none;
}

/* Header */
header {
  height: 70px;
  background: #0d0c0d;
  position: fixed;
  z-index: 1;
  width: 100%;
  img.logo {
    height: 30px;
  }
}

input,
button {
  padding: 0 7.5px;
  height: 25px;
  border: none;
}

input {
  border-radius: 5px 0 0 5px;
}

button {
  border-radius: 0 5px 5px 0;
  i {
    color: rgb(138, 135, 135);
  }
}
</style>
