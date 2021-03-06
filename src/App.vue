<template>
  <div id="app">
    <div class="bg">
      <header class="user-container">
        <img src="../public/to-do-list.svg" class="todo-logo">
        <form @submit.prevent="addTodo(todo)">
          <input type="text" class="todo-text" placeholder="Adicionar novo todo" v-model="todo.description">
          <button class="add-todo">Adicionar</button>
        </form>
      </header>
      <main class="todo-container">
        <Todo v-for="t in todos" :key="t.id" :todo="t" @toggle="toggleTodo" @remove="removeTodo"/>
      </main>
    </div>
  </div>
</template>

<script>
import Todo from './components/Todo'

export default {
  name: 'App',
  data() {
    return {
      todos: [],
      todo: {
        checked: false
      }
    }
  },
  methods: {
    addTodo(todo) {
      todo.id = Date.now()
      this.todos.push(todo)
      this.todo = { checked: false }
    },
    toggleTodo(todo) {
      const index = this.todos.findIndex(item => item.id === todo.id)
      if (index > -1) {
        const checked = !this.todos[index].checked
        this.$set(this.todos, index, { ...this.todos[index], checked })
      }
    },
    removeTodo(todo) {
      const index = this.todos.findIndex(item => item.id === todo.id)
      if (index > -1) {
        this.$delete(this.todos, index)
      }
    }
  },
  components: {
    Todo
  }
}
</script>

<style lang="postcss" scoped>
  #app {
    @apply bg-gray-900 w-screen h-screen pt-4 justify-center;
  }
  
  .bg {
    @apply bg-gray-900 h-auto;
  }
  
  .todo-logo {
    @apply w-12 justify-self-center self-center mb-4;
  }

  .user-container {
    @apply grid w-full box-border justify-center;
  }

  .user-container form {
    @apply flex w-96;
  }

  .todo-text, .add-todo {
    @apply p-3 outline-none rounded-md font-medium;
  }

  .todo-text {
    @apply text-gray-300 font-medium w-full mr-4;
    background-color: rgba(255, 255, 255, 0.1);
  }

  .add-todo {
    @apply bg-gray-300 text-gray-800 duration-300;
    box-shadow: 0 4px 0 rgba(255, 255, 255, 0.6);
  }
  
  .add-todo:hover {
    @apply transform translate-y-1 bg-green-500 text-gray-300;
    box-shadow: 0 4px 0 rgb(5, 150, 105);
  }

  .todo-container {
    @apply flex justify-center items-center w-96 m-auto flex-wrap;
  }
</style>
