<template>
  <div class="bg">
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

<style lang="sass">
.bg
  background: url(assets/top.jpg) no-repeat center center fixed
  -webkit-background-size: cover
  -moz-background-size: cover
  background-size: cover
  -o-background-size: cover
  min-height: 100vh
  position: relative
  height: 100%

</style>
