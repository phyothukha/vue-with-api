<template>
  <div class="input-group mb-3">
    <input
      type="text"
      class="form-control"
      placeholder="Search..."
      v-model="keyWord"
      aria-label="search"
      aria-describedby="basic-addon2"
    />
    <button @click="search" class="btn btn-primary">Search</button>
  </div>
</template>

<script>
import { debounce } from "lodash";
export default {
  data() {
    return {
      keyWord: null,
    };
  },
  methods: {
    search() {
      this.$emit("search", this.keyWord);
    },
  },
  watch: {
    keyWord: debounce(function (newValue) {
      this.$emit("search", newValue);
    }, 500),
  },
};
</script>

<style lang="scss" scoped></style>
