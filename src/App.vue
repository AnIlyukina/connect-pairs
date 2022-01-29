<template>
  <div class="app">
    <img class="app__logo" alt="Vue logo" src="./assets/logo.png">
    <Board/>
  </div>

</template>

<script>
import Board from './components/Board.vue'

export default {
  name: 'App',
  components: {
    Board
  }
}
</script>

<style>
.app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.app__logo{
  width: 150px;
}
</style>
