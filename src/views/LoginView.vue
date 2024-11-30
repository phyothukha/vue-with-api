<template>
  <div class=" row min-vh-100 justify-content-center align-items-center">
    <div class="col-lg-4">
      <div class="card p-3 shadow-sm">
                <h3>Login form</h3>
                <form action="" @submit.prevent="login" ref="loginForm">
                  <div class="mb-3">
                    <label  class="form-label">Email address</label>
                    <input type="email" name="email" v-model="email" class="form-control"  placeholder="name@example.com">
                  </div>
                  <div class="mb-3">
                    <label  class="form-label">Password</label>
                    <input type="password" name="password" class="form-control" placeholder="password">
                  </div>
                  <button class=" btn btn-primary w-100">Login</button>
                 </form>
      </div>
    </div>
  </div>


</template>

<script>

import {mapGetters, mapState} from "vuex";

export default {
  computed: {
    ...mapState([
        "auth",
        "token"
    ]),

    ...mapGetters([
        "getUrl",

    ])
  },

  methods: {
    login() {
      const formData= new FormData(this.$refs.loginForm)
      fetch(this.getUrl('/login'),{
        method: "POST",
        body: formData,
      })
          .then((res)=>res.json()).then(data=>{
              if(data.success){
                this.$store.dispatch("setAuth",data.auth)
                this.$store.dispatch("setToken",data.token)
                this.$router.push('/dashboard');
              }else {

              }



      })
    }
  },
}
</script>

<style lang="scss" scoped>

</style>