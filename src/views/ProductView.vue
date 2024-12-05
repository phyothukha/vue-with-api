<template>
  <div class="container my-5">
    <h1>Product List</h1>
    <hr />

    <table class="table text-center">
      <thead>
        <tr>
          <th>#</th>
          <th>name</th>
          <th>price</th>
          <th>stock</th>
          <th>date</th>
          <th>time</th>
          <th>controls</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="row in rows.data">
          <td>{{ row.id }}</td>
          <td>{{ row.name }}</td>
          <td>{{ row.price }}</td>
          <td>{{ row.stock }}</td>
          <td>{{ row.date }}</td>
          <td>{{ row.time }}</td>
          <td></td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from "axios";
import { mapGetters } from "vuex";

export default {
  data() {
    return {
      rows: {},
    };
  },
  computed: {
    ...mapGetters(["getUrl"]),
  },

  methods: {
    fetchProducts() {
      axios.get(this.getUrl("/products")).then((res) => (this.rows = res.data));
    },
  },

  mounted() {
    this.fetchProducts();
  },
};
</script>

<style lang="scss" scoped></style>
