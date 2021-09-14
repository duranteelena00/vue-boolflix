<template>
  <section :id="id">
    <div class="row justify-content-sm-start">
      <h2 v-if="items.length">{{ title }}</h2>
      <div class="col justify-content-sm-start" v-for="item in items" :key="item.id">
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
  margin-bottom: 40px;
}

h2 {
  margin-bottom: 35px;
  color: #e5e5e5;
}

.col {
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>