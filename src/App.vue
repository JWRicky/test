<script>
import TodoAdd from './components/TodoAdd.vue'

export default {
  components: {
    TodoAdd,
  },
  data() {
    return {
      todos: [{ isDone: false, text: 'ToDoの文字列' }],
    }
  },
  methods: {
    addTodo(newTodoText) {
      if (!newTodoText) return alert('文字を入力してください')
      this.todos.push({
        isDone: false,
        text: newTodoText,
      })
    },
    clearDoneTodos() {
      this.todos = this.todos.filter((todo) => !todo.isDone)
    },
  },
}
</script>

<template>
  <TodoAdd @delete-done="clearDoneTodos" @add-todo="addTodo"/>
  <p v-if="todos.length === 0">ToDoがまだありません！</p>
  <ul v-else>
    <li v-for="todo in todos" :key="todo">
      <input type="checkbox" v-model="todo.isDone" /><span
        :class="{ 'todo-done': todo.isDone }"
        >{{ todo.text }}</span
      >
    </li>
  </ul>
</template>