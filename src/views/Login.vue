<template>
  <div>
    <h1>Login</h1>
    <input v-model="username" placeholder="username">
    <input v-model="password" placeholder="password">
    <button @click="login()">Login</button>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Login',
  data(){
      return{
          username: "",
          password: ""
      }
  },
    methods: {
        login(){
axios.post('http://18.139.50.74:8080/login', {
  username: this.username,
  password: this.password
})
.then((response) => {
  console.log(response);
  alert(response.data.message)
}, (error) => {
  console.log(error);
});
        }
    }
}
</script>
