<template>
  <nav>
    <Navbar />
  </nav>
  <router-view />
</template>

<script>
import * as bootstrap from "bootstrap";
import Navbar from "@/components/Navbar.vue";
import axios from "axios";

export default {
  components: { Navbar },
  created() {
    if (localStorage.getItem("token") && localStorage.getItem("auth")) {
      this.$store.dispatch("setToken", localStorage.getItem("token"));
      this.$store.dispatch("setAuth", JSON.parse(localStorage.getItem("auth")));

      axios.defaults.headers.common["Authorization"] =
        "Bearer " + localStorage.getItem("token");
    }
  },
};
</script>
<style lang="scss">
@import "app.scss";
</style>
