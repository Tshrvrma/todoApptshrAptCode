<!-- <template>
  <div id="app">
    <todo-app></todo-app>
  </div>
</template>

<script>
import TodoApp from './components/TodoApp.vue'

export default {
  name: 'App',
  components: {
    TodoApp
  }
}
</script>

<style scoped>
#app {
  background-color: #001f3f;
  width: auto;
  min-height: 100vh; 
}

todo-app {
  height: auto; 
}
</style> -->

<template>
  <div id="app">
    <TodoApp />
  </div>
</template>

<script>
import TodoApp from './components/TodoApp.vue';

export default {
  name: 'App',
  components: {
    TodoApp
  }
}
</script>

<style>
#app {
  font-family: Arial, sans-serif;
  text-align: center;
  background-color: #001f3f;
  width: auto;
  min-height: 100vh; 
  overflow:hidden;
}
todo-app {
  height: auto; 
}
</style>

