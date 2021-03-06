<template>
  <div id="app">
    <Todo/>
  </div>
</template>

<script>
import Todo from './components/Todo'

export default {
  name: 'App',

  components: {
    Todo
  }
}
</script>

<style lang="postcss" scoped>
  #app {
    @apply flex bg-black w-screen h-screen pt-10 justify-center;
  }
</style>
