<template>
  <div id="app">
    <Header> </Header>
    <Dashboard> </Dashboard>
  </div>
</template>

<script>
import Header from './components/Header.vue';
import Dashboard from './components/Dashboard.vue';


export default {
  name: 'app',
  components: {
    Header,
    Dashboard
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  /* margin-top: 60px; */
}

body {
  margin: 0;
  padding: 0;
}
</style>
