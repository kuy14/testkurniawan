<template>
  <div>
    <h1>Register</h1>
    <input v-model="username" placeholder="username">
    <input v-model="email" placeholder="email">
    <input v-model="password" placeholder="password" type="password">
    <button @click="register">Register</button>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'Register',
    data(){
      return{
          username: "",
          email:"",
          password: ""
      }
  },
    methods: {
        register(){
axios.post('http://18.139.50.74:8080/register', {
  username: this.username,
  email: this.email,
  password: this.password
})
.then((response) => {
  console.log(response);
  alert(response.data.message)
  if(response.status === 200){
      this.router.push({ path: '/login' })
  }
}, (error) => {
  console.log(error);
});
        }
    }
}

</script>