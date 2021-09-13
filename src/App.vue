<template>
  <div id="app">
    <header>
      <div class="container">
        <img src="@/assets/images/Boolflix_logo.png" alt="" />
        <Search @search="getResults" />
      </div>
    </header>
    <main>
      <div class="container">
        <div class="card-container">
          <ul class="card" v-for="item in results" :key="item.id">
            <li>title: "{{ item.title || item.name }}"</li>
            <li v-if="item.original_title || item.original_name">
              original title: "{{ item.original_title || item.original_name }}"
            </li>
            <li class="flag">
              <img
                v-if="flags.includes(item.original_language)"
                :src="getFlags(item.original_language)"
                alt=""
              />
              <span v-else>lang: {{ item.original_language }} </span>
            </li>
            <li class="stars">
              <ul>
                <li v-if="(item.vote_average / 2).toFixed() > 0">
                  <i class="fas fa-star"></i>
                </li>
                <li v-else>
                  <i class="far fa-star"></i>
                </li>
                <li v-if="(item.vote_average / 2).toFixed() > 1">
                  <i class="fas fa-star"></i>
                </li>
                <li v-else>
                  <i class="far fa-star"></i>
                </li>
                <li v-if="(item.vote_average / 2).toFixed() > 2">
                  <i class="fas fa-star"></i>
                </li>
                <li v-else>
                  <i class="far fa-star"></i>
                </li>
                <li v-if="(item.vote_average / 2).toFixed() > 3">
                  <i class="fas fa-star"></i>
                </li>
                <li v-else>
                  <i class="far fa-star"></i>
                </li>
                <li v-if="(item.vote_average / 2).toFixed() > 4">
                  <i class="fas fa-star"></i>
                </li>
                <li v-else>
                  <i class="far fa-star"></i>
                </li>
              </ul>
            </li>
            <li v-if="item.overview">overview: {{ item.overview }}</li>
            <li>
              <img
                class="poster"
                v-if="item.poster_path"
                :src="`${imgUri + item.poster_path}`"
                alt=""
              />
              <div class="poster-placeholder" v-else>
                <img src="@/assets/images/poster_placeholder.png" alt="" />
              </div>
            </li>
          </ul>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
import axios from "axios";

import Search from "@/components/Search.vue";

export default {
  name: "App",
  components: {
    Search,
  },
  data() {
    return {
      movies: [],
      series: [],
      api: {
        key: "cfc0856a6e486ed1f7367bd371b61e4e",
        baseUri: "https://api.themoviedb.org/3",
      },
      flags: ["en", "it"],
      imgUri: "https://image.tmdb.org/t/p/w342/",
      posterVisibility: true,
      infoVisibility: false,
    };
  },
  computed: {
    results() {
      return [...this.movies, ...this.series];
    },
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
        // metto le quadre perché il nome dell'ogetto è dinamico (this.movies / this.series)
        this[entity] = res.data.results;
      });
    },
    getFlags(lang) {
      return require(`@/assets/images/${lang}.png`);
    },
    flipCard() {
      this.posterVisibility = true;
      this.infoVisibility = false;
    },
  },
};
</script>

<style>
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
  font-family: Helvetica, Arial, sans-serif;
  background-color: #111010;
}

.container {
  height: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.card-container {
  display: flex;
  flex-wrap: wrap;
}

ul {
  list-style-type: none;
}

header {
  height: 70px;
  background: #0d0c0d;
  position: fixed;
  z-index: 1;
  width: 100%;
}

header img {
  height: 30px;
}

.card-container {
  display: flex;
  justify-content: center;
  align-items: center;
}

.card {
  margin-bottom: 125px;
  padding: 10px 30px 0 15px;
  height: 400px;
  width: 342px;
  display: flex;
  flex-direction: column;
  position: relative;
}

.card li {
  padding: 2.5px 0;
}

.card li.flag > img {
  margin-top: 7.5px;
  width: 40px;
  height: 20px;
  object-fit: cover;
  object-position: center;
}

.card img.poster {
  height: 470px;
  width: 322px;
  object-fit: cover;
  border-radius: 5px;
  position: absolute;
  top: 0;
  left: 0;
}

.card img.poster:hover {
  opacity: 0.1;
  transform: scale(1.1);
  border: 1px solid white;
}

.card .poster-placeholder {
  height: 470px;
  width: 322px;
  object-fit: cover;
  border-radius: 5px;
  position: absolute;
  top: 0;
  left: 0;
  border: 1px solid rgba(255, 255, 255, 0.1);
}

.card .poster-placeholder > img {
  width: 50px;
  position: absolute;
  left: 15px;
  bottom: 10px;
  opacity: 0.3;
}

li.stars ul {
  padding: 0;
  display: flex;
  flex-direction: row;
  list-style-type: none;
}

li.stars i {
  color: gold;
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
}

button i {
  color: rgb(138, 135, 135);
}

main {
  padding-top: 100px;
  font-size: 15.5px;
  color: white;
}
</style>
