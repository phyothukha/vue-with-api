<template>
  <div class="container my-5">
    <h1>Product List</h1>
    <hr />

    <table class="table text-center align-middle">
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
          <td>
            <div class="btn btn-group">
              <button
                @click="fetchProduct(row.id)"
                class="btn btn-outline-primary"
              >
                <i class="bi bi-info-circle"></i>
              </button>
              <button class="btn btn-outline-primary">
                <i class="bi bi-pencil"></i>
              </button>
              <button
                @click="deleteProduct(row.id)"
                class="btn btn-outline-primary"
              >
                <i class="bi bi-trash"></i>
              </button>
            </div>
          </td>
        </tr>
      </tbody>
    </table>

    <Pagination :links="rows?.meta?.links" @fetchLink="fetchProducts" />
  </div>
</template>

<script>
import Pagination from "@/components/Pagination.vue";
import axios from "axios";
import Swal from "sweetalert2/dist/sweetalert2";
import { mapGetters } from "vuex";

export default {
  data() {
    return {
      rows: {},
    };
  },
  components: {
    Pagination,
  },
  computed: {
    ...mapGetters(["getUrl"]),
  },

  methods: {
    showToast(icon, message) {
      Swal.mixin({
        toast: true,
        position: "top-end",
        showConfirmButton: false,
        timer: 3000,
        timerProgressBar: true,
        didOpen: (toast) => {
          toast.onmouseenter = Swal.stopTimer;
          toast.onmouseleave = Swal.resumeTimer;
        },
      }).fire({
        icon,
        title: message,
      });
    },
    fetchProducts(url) {
      axios.get(url).then((res) => (this.rows = res.data));
    },
    fetchProduct(id) {
      axios.get(this.getUrl("/products/" + id)).then((res) => console.log(res));
    },
    deleteProduct(id) {
      axios.delete(this.getUrl("/products/" + id)).then((res) => {
        this.fetchProducts(
          this.rows.meta.links.find((link) => link.active == true).url
        );
        this.showToast("success", res.data.message);
      });
    },
  },

  mounted() {
    this.fetchProducts(this.getUrl("/products"));
  },
};
</script>

<style lang="scss" scoped></style>
