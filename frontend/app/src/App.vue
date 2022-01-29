<template>
  <div>
    <img alt="Vue logo" src="./assets/logo.png">
    <Contract />
  </div>
</template>

<script>
import Contract from './components/Contract.vue'

export default {
  name: 'App',
  components: {
    Contract
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
