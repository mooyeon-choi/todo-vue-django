<template>
  <div class="LoginForm">
    <!-- 
        form에 이벤트 리스너 달아서,
        1) 사용자 입력값 출력
        2) /api-token-auth/로 요청 보내서 토큰값 출력
    -->
    <form @submit.prevent="login">
      <label for="username">username: </label>
      <input v-model="credentials.username" type="text" id="username"><br>
      <label for="password">password: </label>
      <input v-model="credentials.password" type="password" id="password"><br>
      <input type="submit" value="로그인">
    </form>
  </div>
</template>

<script>
import axios from 'axios'
import router from '../router'

export default {
    name: 'LoginForm',
    data() {
        return {
            credentials: {}
        }
    },
    methods: {
        login() {
            axios.post('http://127.0.0.1:8000/api-token-auth/', this.credentials)
                .then(response => {
                    console.log(response)
                    const token = response.data.token
                    this.$session.start()
                    this.$session.set('jwt', token)
                    router.push('/')
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