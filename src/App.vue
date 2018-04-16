<template>
  <div id="app">
    <Header />
    <Todo />
  </div>
</template>

<script>
import Header from './components/Header'
import Todo from './components/Todo'

export default {
  name: 'App',
  components: {
    Todo,
    Header
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
body {
  margin: 0px;
  background-image: linear-gradient( 135deg, #97ABFF 10%, #123597 100%);
}
</style>
