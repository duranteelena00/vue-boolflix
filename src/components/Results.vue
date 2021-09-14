<template>
  <section :id="id">
    <div class="row">
    <h2>{{ title }}</h2>
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
h2 {
  margin-bottom: 40px;
}

.col {
   display: flex;
    justify-content: center;
    align-items: center;
}

</style>