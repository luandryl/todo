<template>
  <div id="app">
    <todo></todo>
  </div>
</template>

<script>
import Todo from './components/todo'

export default {
  name: 'app',
  components: {
    Todo
  }
}
</script>

<style>
body {
  background: #F7F7F7;
}
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  padding: 2rem;
}
</style>
