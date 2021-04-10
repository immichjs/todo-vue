<template>
  <div id="app" class="flex flex-col items-center justify-center h-screen gap-5 px-3">
    <div class="relative w-full h-auto p-5 rounded-md md:w-2/4 app-container">
      <header class="user-container">
        <div
          v-if="showNewTodo"
          class="fixed top-0 left-0 z-10 flex flex-col items-center justify-center w-screen h-screen gap-3 px-64"
          >
          <input
            type="text"
            class="w-full p-5 font-medium text-gray-300 rounded-md shadow-sm outline-none"
            placeholder="Escreve aqui seu novo item na lista ..."
            v-model="todo.description"
          >
          <button 
            class="w-1/4 p-2 font-medium text-white rounded-md"
            @click="addTodo(todo)">Adicionar</button>
        </div>
        <button 
          title="Adicionar um novo item"
          class="absolute flex items-center gap-3 p-4 ml-5 text-base font-medium text-white duration-200 bg-green-600 rounded-full bottom-1/2 md:left-full drop-shadow-sm hover:bg-green-700"
          @click="showAdd"
        >
          <img src="@/assets/add.svg" alt="Adicionar novo Todo" class="w-5">
        </button>
      </header>
      <main class="px-10 todo-container">
        <Todo v-for="t in todos" :key="t.id" :todo="t" @toggle="toggleTodo" @remove="removeTodo" />
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
      },
      showNewTodo: false
    }
  },
  components: {
    Todo,
  },
  methods: {
    showAdd() {
      this.showNewTodo = true
    },
    findIndexInTodoItems(argItem) {
      const index = this.todos.findIndex(item => item.id === argItem.id)
      return index
    },
    addTodo(todo) {
        this.showNewTodo = false
        todo.id = Date.now()
        this.todos.push(todo)
        this.todo = { checked: false }
    },
    toggleTodo(todo) {
      const index = this.findIndexInTodoItems(todo)

      if (index > -1) {
        const checked = !this.todos[index].checked
        this.$set(this.todos, index, { ...this.todos[index], checked })
      }
    },
    removeTodo(todo) {
      const index = this.findIndexInTodoItems(todo)
      
      if (index > -1) this.$delete(this.todos, index)
    },
  }
}
</script>

<style scoped>
#app {
  background: #343A40;
  /* background: linear-gradient(-30deg, rgba(240,98,146,1) 0%, rgba(229,92,138,1) 50%, rgba(229,92,138,1) 100%); */
}

.app-container {
  background: #3C424A;
}

header input {
  background: #343A40;
}

header button {
  outline: none;
}

header div {
  background: rgba(0, 0, 0, 0.5);
}

header div button {
  background: #373C44;
  transition: .2s;
  outline: none;
}

header div button:hover {
  background: #f06292;
}
</style>
