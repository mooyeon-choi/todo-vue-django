<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <!-- 이벤트 리스너 등록 -->
    <TodoForm @todoCreate-event="todoCreate"/> <!-- PascalCase, uppercamelcase -->
    <!-- kebab-case -->
    <TodoList :todos="todos"/>
  </div>
</template>

<script>
// @ is an alias to /src
import axios from 'axios' // python에서 'import request' 같은
// import jwtDecode from 'jwt-decode'
import { mapGetters } from 'vuex' // python에서 'from bs4 import BeautifulSoup' 같은
import router from '../router'

import TodoList from '@/components/TodoList.vue'
import TodoForm from '@/components/TodoForm.vue'

export default {
  name: 'home',
  components: {
    TodoList,
    TodoForm
  },
  data() {
    // 컴포넌트에서는 반드시 data를 함수로 작성하고, object를 리턴한다
    return {
      todos: [],
    }
  },
  computed: {
    ...mapGetters([
      'options',
      'user'
    ])
    // options() {
    //   return this.$store.getters.options
    // },
    // user() {
    //   return this.$store.getters.user
    // }
  },
  methods: {
    todoCreate(title) {
      console.log('==부모컴포넌트==')
      console.log(title)
      // axios 요청 POST /todos/
      // this.$session.start()
      // const token = this.$session.get('jwt')
      // const options = {
      //   headers: {
      //     Authorization: `JWT ${token}` // JWT 뒤에 공백 필수!!
      //   }
      // }
      // console.log(jwtDecode(token))
      const data = {
        title: title,
        user: this.user
      }
      // request.POST인 경우는 반드시 FormData!
      // const formData = new FormData()
      // formData.append('title', title)
      // formData.append('user', 1)
      axios.post('http://127.0.0.1:8000/api/v1/todos/', data, this.options)
        .then(response => {
          console.log(response)
          this.todos.push(response.data)
        })
        .catch(error => {
          console.log(error)
        })
    },
    getTodos() {
      // axios 요청
      // this.$session.start()
      // const token = this.$session.get('jwt')
      // const options = {
      //   headers: {
      //     Authorization: `JWT ${token}` // JWT 뒤에 공백 필수!!
      //   }
      // }
      axios.get(`http://127.0.0.1:8000/api/v1/users/${this.user}/`, this.options)
        .then(response => {
          console.log(response) // 만약, 오류가 발생한다면 ESLint 설정을 package.json에 추가
          this.todos = response.data.todo_set
        })
        .catch(error => {
          console.log(error)
        })      
    },
    isLogin() {
      this.$session.start()
      // session에 jwt가 없다면, 즉 토큰이 없다면, 비로그인이라면,
      if (!this.$session.has('jwt')) {
        router.push('/login')
      } else {
        // 로그인 되어있다면, vuex token 업데이트
        this.$store.dispatch('login', this.$session.get('jwt'))
      }
    }
  },
  mounted() {
    this.isLogin() // 로그인 되어있으면
    this.getTodos() // 가져온다.
  }
}
</script>
