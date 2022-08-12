<template>
  <div id="app">
    <todo-app></todo-app>
  </div>
</template>
<script >
import TodoApp from './components/TodoApp.vue'
  export default{
    name: "app",
    components: { TodoApp }
  }
</script>
<style scoped>

</style>
