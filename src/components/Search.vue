<template>
  <div>
    <input
      type="text"
      placeholder="Inserisci film o serie tv..."
      v-model.trim="inputValue"
      @keyup.enter="emitSearch"
    />
    <button
      type="submit"
      class="btn btn-secondary"
      data-toggle="tooltip"
      data-placement="left"
      title="Tooltip on left"
      @click="emitSearch"
    >
      <i class="fas fa-search ps-2 pe-2"></i>
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

<style lang="scss" scoped>
div {
  display: flex;
  align-items: center;
}

input,
button {
  padding: 0 7.5px;
  height: 38px;
  background: transparent;
  border: none;
}

input {
  border: 1px solid white;
  color: white;
}

button { 
  i {
    color: white;
    font-size: 25px;
  }
}

</style>