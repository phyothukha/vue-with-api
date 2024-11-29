<template>
  <nav>
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link>
  </nav>
  <router-view />
</template>


<script>
import * as bootstrap from "bootstrap";

export default {
  
}

</script>
<style lang="scss">
@import "app.scss";
</style>
