<template>
  <div class="container my-5">
    <h1>Product Create</h1>
    <hr />
    <form action="" @submit.prevent="addProducts" ref="productCreate">
      <div class="row">
        <div class="col">
          <div class="mb-3">
            <Input label="Input Name" name="name" :errors="errors" />
          </div>
        </div>
        <div class="col">
          <div class="mb-3">
            <Input type="number" name="price" label="Price" :errors="errors" />
          </div>
        </div>
        <div class="col">
          <div class="mb-3">
            <Input type="number" name="stock" label="Stock" :errors="errors" />
          </div>
        </div>
        <div class="col-12">
          <div class="mb-3">
            <label for="photos" class="form-label">File Upload</label>
            <input
              type="file"
              multiple
              name="photos[]"
              class="form-control"
              :class="{ 'is-invalid': errors.photos }"
            />
            <div class="invalid-feedback" v-if="errors.photos">
              {{ errors.photos[0] }}
            </div>
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
          Add product
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
      const formData = new FormData(this.$refs.productCreate);

      axios
        .post(this.getUrl("/products"), formData)
        .then((res) => {
          this.errors = {};
          this.showToast("success", "create successfully!");
          this.$refs.productCreate.reset();
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
};
</script>

<style lang="scss" scoped></style>
