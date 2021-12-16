<template>
  <section :id="id">
    <div class="container-fluid align-content-between">
      <div class="row justify-content-sm-start">
        <h2 v-if="items.length">{{ title }}</h2>
        <div
          class="col-2 justify-content-sm-start"
          v-for="item in items"
          :key="item.id"
        >
          <Card :item="item" />
        </div>
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

<style scoped lang="scss">
section {
  .container-fluid {
    padding: 30px;
    height: calc(100vh - 70px);
    overflow-y: auto;
    .row {
      margin-bottom: 40px;
      h2 {
        margin-bottom: 20px;
        color: #e5e5e5;
      }
      .col {
        display: flex;
        justify-content: center;
      }
    }
  }
}
</style>