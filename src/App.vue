<template>
  <div id="app">
    <div class="bg">
      <header class="user-container">
        <img src="../public/to-do-list.svg" class="todo-logo">
        <form @submit.prevent="addTodo(todo)">
          <input type="text" class="todo-text" placeholder="Adicionar um novo todo" v-model="todo.description" ref="todoInput">
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
      const todoInput = this.$refs['todoInput'].value
      if (todoInput && todoInput !== ' ') {
        todo.id = Date.now()
        this.todos.push(todo)
        this.todo = { checked: false }
      } else {
        alert('É necessário escrever alguma coisa para adicionar um novo Todo.')
      }
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
    @apply flex flex-col w-full pr-5 pl-5 sm:grid lg:justify-center;
  }

  .user-container form {
    @apply grid gap-3 sm:flex;
  }

  .todo-text, .add-todo {
    @apply p-3 lg:p-5 outline-none rounded-md font-medium text-xl;
  }

  .todo-text {
    @apply text-gray-300 font-medium w-full lg:w-96;
    background-color: rgba(255, 255, 255, 0.1);
    box-shadow: 0 4px 0 rgba(255, 255, 255, 0.05);
  }

  .add-todo {
    @apply bg-gray-300 text-gray-800 duration-300 lg:hover:bg-green-500 lg:hover:text-gray-300 transform lg:hover:translate-y-1;
    box-shadow: 0 4px 0 rgba(255, 255, 255, 0.6);
  }
  
  .add-todo:hover {
    box-shadow: 0 4px 0 rgb(5, 150, 105);
  }

  .todo-container {
    @apply flex justify-center items-center pr-5 pl-5 lg:m-auto lg:p-0 flex-wrap;
  }

  @media only screen and (min-width: 1024px) {
    .todo-container {
      width: 32.5rem;
    }
  }
</style>
