<template>
  <div>
    <input
      type="text"
      placeholder="Inserisci film o serie tv..."
      v-model.trim="inputValue"
      @keyup.enter="emitSearch"
    />
    <button type="submit" @click="emitSearch">
      <i class="fas fa-search"></i>
    </button>
  </div>
</template>

<script>
export default {
  name: "Search",
  data() {
    return {
      inputValue: "",
    };
  },
  methods: {
    emitSearch() {
      this.$emit("search", this.inputValue);
    },
  },
};
</script>

<style scoped>
</style>