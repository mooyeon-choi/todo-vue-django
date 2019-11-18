<template>
  <div class="todo-list">
      <h2>투두</h2>
      <li
        v-for="todo in todos"
        :key="todo.id"      
      >
        {{ todo.title }}
      </li>
  </div>
</template>

<script>

export default {
    name: 'TodoList',
    props: {
      todos: {
        type: Array,
        required: true,
      }
    }
}
</script>

<style>

</style>