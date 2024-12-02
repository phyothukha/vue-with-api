<template>
  <nav>
    <Navbar />
  </nav>
  <router-view />
</template>

<script>
import * as bootstrap from "bootstrap";
import Navbar from "@/components/Navbar.vue";

export default {
  components: { Navbar },
  created() {
    if (localStorage.getItem("token") && localStorage.getItem("auth")) {
      this.$store.dispatch("setToken", localStorage.getItem("token"));
      this.$store.dispatch("setAuth", JSON.parse(localStorage.getItem("auth")));
    }
  },
};
</script>
<style lang="scss">
@import "app.scss";
</style>
