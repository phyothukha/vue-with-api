<template>
  <div>
   <div class=" row min-vh-100 justify-content-center align-items-center">
     <div class="col-lg-4">
       <div class="card p-3 shadow-sm">
       <h3>Register form</h3>
       <form action="" @submit.prevent="register" ref="registerForm">
       <div class="mb-3">
         <label  class="form-label">Your Name</label>
         <input type="text" name="name" v-model="name" class="form-control"  placeholder="name">
       </div>
         <div class="mb-3">
           <label  class="form-label">Email address</label>
           <input type="email" name="email" v-model="email" class="form-control"  placeholder="name@example.com">
         </div>
         <div class="mb-3">
           <label  class="form-label">Password</label>
           <input type="password" name="password" class="form-control" placeholder="password">
         </div>
         <div class="mb-3">
           <label  class="form-label">Confirm Password</label>
           <input type="password" name="password_confirmation" class="form-control"  placeholder="Password Confirmation">
         </div>
         <button class=" btn btn-primary w-100">Register</button>
       </form>
       </div>
     </div>
   </div>


  </div>
</template>

<script>
import {mapGetters, mapState} from "vuex";
import router from "@/router";

    export default {
      computed: {
        ...mapState([
            "apiUrl",
        ]),
        ...mapGetters([
            "getUrl",
        ])

      },
      methods: {
        register() {
          let formData = new FormData(this.$refs.registerForm);
          fetch(this.getUrl('/register'),{
          method: "POST",
          body: formData,
        }).then(res=>res.json()).then(data=>{
          if(data.success){
            this.$router.push('/login');
          }
        })


          // console.log(formData.get('name'),formData.get('email'));

        }
      },
    }
</script>

<style lang="scss" scoped>

</style>