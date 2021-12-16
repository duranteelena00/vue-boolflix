<template>
  <div class="card d-flex justify-content-center">
    <ul class="card-body" :key="item.id">
      <li class="title">
        <h1>{{ item.title || item.name }}</h1>
      </li>
      <li>
        <img
          class="flag"
          v-if="
            item.original_language === 'it' || item.original_language === 'en'
          "
          :src="flagPath"
          alt=""
        />
        <span class="lang" v-else>{{ item.original_language }}</span>
      </li>
      <li class="stars">
        <i
          v-for="n in 5"
          :key="n"
          :class="n <= vote ? 'fas' : 'far'"
          class="fa-star"
        ></i>
      </li>
      <li class="overview" v-if="item.overview">
        {{ item.overview }}
      </li>
      <li class="image">
        <img
          class="poster"
          v-if="item.poster_path"
          :src="`${imgUrl + item.poster_path}`"
          alt=""
        />
        <div class="poster-placeholder-container" v-else>
          <img
            class="poster-placeholder"
            src="@/assets/images/poster_placeholder.png"
            alt=""
          />
          <h1>{{ item.title || item.name }}</h1>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "Card",
  data() {
    return {
      flags: ["en", "it"],
      imgUrl: "https://image.tmdb.org/t/p/w342/",
    };
  },
  props: ["item"],
  computed: {
    flagPath() {
      return require(`@/assets/images/${this.item.original_language}.png`);
    },
    vote() {
      return Math.ceil(this.item.vote_average / 2);
    },
  },
};
</script>

<style lang="scss" scoped>
.card {
  margin-bottom: 40px;
  width: 100%;
  height: 260px;
  position: relative;
  display: flex;
  align-content: flex-start;
  flex-direction: column;
  .card-body > li:not(.image) {
    display: none;
  }
  li {
    margin: 7.5px 0;
  }
  img.flag {
    width: 40px;
    height: 20px;
  }
  .stars {
    display: flex;
    flex-direction: row;
    list-style-type: none;
    i {
      color: gold;
    }
  }
  .overview {
    margin-top: 15px;
    line-height: 22px;
    text-align: justify;
  }
  img.poster {
    width: 100%;
    height: 260px;
    object-fit: cover;
    object-position: top;
    position: absolute;
    top: 0;
    left: 0;
  }
  .poster-placeholder-container {
    height: 260px;
    width: 100%;
    object-fit: cover;
    position: absolute;
    top: 0;
    left: 0;
    border: 1px solid rgba(255, 255, 255, 0.1);
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    align-items: center;
    padding: 7.5px 2.5px 0 0;
    h1 {
      margin: 35px;
      color: rgb(172, 169, 169);
    }
    img.poster-placeholder {
      width: 95%;
      opacity: 0.3;
    }
    h1 {
      margin-bottom: 15px;
    }
  }
}

/* Effects */
.card:active {
  margin: 0;
  width: 50vw;
  height: 100vh;
  background: #111010;
  font-size: 16px;
  position: absolute;
  top: 0px;
  left: 50%;
  transform: translateX(-50%);
  z-index: 3;
}

.card:target .card-body {
  width: 100%;
}

.card:active .card-body:not(.image) {
  margin-top: 60vh;
  padding-top: 15px;
  height: 40vh;
  overflow-y: auto;
}

.card:active .card-body > li:not(.image) {
  display: block;
  padding: 0 35px;
}

.card:active .poster,
.card:target .poster {
  height: 60vh;
}

.card:active .poster-placeholder-container {
  height: 60vh;
  h1 {
    display: none;
  }
}

.card:active .poster-placeholder {
  height: 100%;
  width: auto;
}

.card:active .overview {
  margin-top: 15px;
  max-width: 100%;
  z-index: 2;
  padding-right: 15px;
}
</style>