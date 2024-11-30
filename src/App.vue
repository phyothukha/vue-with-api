<template>
  <nav>
<!--    <router-link to="/">Home</router-link> |-->
<!--    <router-link to="/about">About</router-link>|-->
<!--    <router-link to="/login">Login</router-link>|-->
<!--    <router-link to="/register">Register</router-link>-->
    <Navbar/>
  </nav>
  <router-view />
</template>


<script>
import * as bootstrap from "bootstrap";
import Navbar from "@/components/Navbar.vue";

export default {
  components: {Navbar}

}

</script>
<style lang="scss">
@import "app.scss";
</style>
