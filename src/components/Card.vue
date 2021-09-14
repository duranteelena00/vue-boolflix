<template>
  <ul class="card" :key="item.id">
    <li class="title">title: "{{ item.title || item.name }}"</li>
    <li class="original-title" v-if="item.original_title || item.original_name">
      original title: "{{ item.original_title || item.original_name }}"
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
    <li class="overview" v-if="item.overview">overview: {{ item.overview }}</li>
    <li>
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
      </div>
    </li>
  </ul>
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
  margin-bottom: 125px;
  padding: 25px 45px 0 25px;
  height: 400px;
  width: 342px;
  position: relative;
  display: flex;
  flex-direction: column;
  &:hover {
    transform: scale(1.1);
    font-size: 17px;
  }
  &:hover img.poster {
    opacity: 0.1;
    border: 1px solid white;
  }
  &:hover .overview {
    z-index: 2;
    padding-right: 15px;
  }
  li {
    padding: 2.5px 0;
  }
  .title,
  .original-title {
    width: 210px;
  }
  img.flag {
    margin-top: 7.5px;
    width: 40px;
    height: 20px;
    object-fit: cover;
    object-position: center;
  }
  .stars {
    padding: 5px 0 0 0;
    display: flex;
    flex-direction: row;
    list-style-type: none;
    i {
      color: gold;
    }
  }
  .overview {
    margin-top: 35px;
    padding: 0;
    min-height: 100px;
    max-height: 330px;
    overflow-y: auto;
    line-height: 22px;
    text-align: justify;
  }
  img.poster {
    height: 470px;
    width: 322px;
    object-fit: cover;
    border-radius: 5px;
    position: absolute;
    top: 0;
    left: 0;
  }
  .poster-placeholder-container {
    height: 470px;
    width: 322px;
    object-fit: cover;
    border-radius: 5px;
    position: absolute;
    top: 0;
    left: 0;
    border: 1px solid rgba(255, 255, 255, 0.1);
    display: flex;
    justify-content: flex-end;
    align-items: flex-start;
    padding: 7.5px 2.5px 0 0;
    img.poster-placeholder {
      width: 80px;
      opacity: 0.15;
    }
  }
}
</style>