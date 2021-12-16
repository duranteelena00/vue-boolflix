<template>
  <div id="app">
    <header>
      <div class="container">
        <img class="logo" src="@/assets/images/Boolflix_logo.png" alt="" />
        <div class="d-flex align-items-center">
        <Search class="mx-3" @search="getResults" />
        <i class="fas fa-bell mx-3"></i>
          <img class="user-icon ms-3" src="@/assets/images/user_icon.png" alt="" />
        </div>
      </div>
    </header>
    <div class="main">
      <div class="container-fluid">
        <Results title="Film" id="film" :items="movies" />
        <Results title="Serie TV" id="series" :items="series" />
      </div>
    </div>
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
        console.dir(res)
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


body {
  padding-top: 70px;
  width: 100vw;
  max-height: 100vh;
  overflow: hidden;
  background-color: black;
  font-family: sans-serif, Helvetica, Arial;
  color: white;
}

ul {
  list-style-type: none;
}

/* Header */
header {
  width: 100%;
  height: 70px;
  background: #0d0c0d;
  position: absolute;
  top: 0;
  z-index: 1;
  .container {
    height: 100%;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  img.logo {
    height: 40px;
  }
  div>i {
    font-size: 30px;
  }
  img.user-icon {
    height: 50px;
    border-radius: 7.5px;
  }
}

/* Main */
main {
  .container {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }
}

</style>
