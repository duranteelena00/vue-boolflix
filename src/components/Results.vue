<template>
  <section :id="id">
    <h2>{{ title }}</h2>
    <div class="row flex-column">
      <div class="col" v-for="item in items" :key="item.id">
        <Card :item="item" />
      </div>
    </div>
  </section>
</template>

<script>
import Card from "@/components/Card.vue";

export default {
  name: "Results",
  components: {
    Card,
  },
  props: ["id", "title", "items"],
};
</script>

<style scoped>
.row {
  margin-top: 125px;
}
</style>