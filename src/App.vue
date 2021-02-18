<template>
  <div id="app">
    <Header/>
      <main class="todo-container">
        <div class="todo-list">

        <div v-for="t in todos" :key="t.id">
            <div class="tile-icon">
              <div>
                <i class="icon"></i>
              </div>
            </div>
            <div class="tile-content">
              <p class="tile-subtitle">{{ t.description }}</p>
            </div>

            <div class="tile-action">
              <button class="btn-link">Concluído</button>
              <button class="btn-link"><span>Remover</span></button>
            </div>
          </div>
        </div>
      </main>
  </div>
</template>

<script>
import Header from './components/Header'

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
    }
  },

  components: {
    Header
  }
}
</script>

<style lang="postcss" scoped>
  #app {
    @apply bg-black w-screen h-screen pt-10;
  }

  .todo-container {
    @apply flex justify-center w-full;
  }

  .todo-list {
    @apply p-3 w-96 rounded-md;
    background-color: rgba(255, 255, 255, 0.1);
  }
</style>
