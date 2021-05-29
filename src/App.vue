<template>
  <div id="app">
      <PageSearch></PageSearch>
  </div>
</template>

<script>
import PageSearch from './components/PageSearch.vue'

export default {
    name: 'App',
    components: {
        PageSearch
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
