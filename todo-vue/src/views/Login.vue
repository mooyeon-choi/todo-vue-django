<template>
  <div class="login">
      <h2>로그인</h2>
      <login-form @login-event="login"/>
  </div>
</template>

<script>
import LoginForm from '../components/LoginForm.vue'
import axios from 'axios'

export default {
    name: 'Login',
    components: {
        LoginForm
    },
    methods: {
        login(credentials) {
            axios.post('http://127.0.0.1:8000/api-token-auth/', credentials)
                .then(response => {
                    console.log(response)
                    const token = response.data.token
                    this.$session.start()
                    this.$session.set('jwt', token)
                })
                .catch(error => {
                    console.log(error)
                })
        }
    }
}
</script>

<style>

</style>