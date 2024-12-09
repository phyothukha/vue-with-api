<template>
  <div class="container my-5">
    <h1>Product Create</h1>
    <hr />
    <form action="" @submit.prevent="addProducts" ref="productUpdate">
      <div class="row">
        <div class="col">
          <div class="mb-3">
            <Input
              label="Input Name"
              :value="product?.name"
              name="name"
              :errors="errors"
            />
          </div>
        </div>
        <div class="col">
          <div class="mb-3">
            <Input
              type="number"
              :value="product.price"
              name="price"
              label="Price"
              :errors="errors"
            />
          </div>
        </div>
        <div class="col">
          <div class="mb-3">
            <Input
              type="number"
              :value="product.stock"
              name="stock"
              label="Stock"
              :errors="errors"
            />
          </div>
        </div>
      </div>

      <div class="col-12 text-center">
        <button type="submit" :disabled="isLoading" class="btn btn-primary">
          <span
            v-if="isLoading"
            class="spinner-grow spinner-grow-sm"
            aria-hidden="true"
          ></span>
          Update product
        </button>
      </div>
    </form>
  </div>
</template>

<script>
import Input from "@/components/Input";
import axios from "axios";
import { mapGetters } from "vuex";
import Swal from "sweetalert2/dist/sweetalert2.js";

export default {
  components: { Input },

  data() {
    return {
      errors: {},
      isLoading: false,
      product: {},
    };
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

    addProducts() {
      this.isLoading = true;
      const formData = new FormData(this.$refs.productUpdate);

      axios
        .put(
          this.getUrl("/products/" + this.$route.params.id),
          new URLSearchParams(formData).toString()
        )
        .then((res) => {
          this.errors = {};
          this.showToast("success", res.data.message);
          this.$refs.productUpdate.reset();
          this.product = res.data.data;
          this.$router.push("/products");
        })
        .catch((err) => {
          console.log(err);
          if (err.response.status == 422) {
            this.errors = err.response.data.errors;
            this.showToast("error", err.response.data.message);
          }
        })
        .finally((_) => (this.isLoading = false));
    },
  },

  mounted() {
    axios
      .get(this.getUrl("/products/" + this.$route.params.id))
      .then((res) => (this.product = res.data.data));
  },
};
</script>

<style lang="scss" scoped></style>
