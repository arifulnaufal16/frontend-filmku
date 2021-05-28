<template>
  <div id="app">
      <div>
        <Search msg="Welcome to Your Vue.js App"/>
      </div>
      <hr>
      
      <div class="container d-flex">
          <div class="row">
            <div v-for="item in 10" :key="item.id" class="w-25">
                <Card></Card>       
            </div>
          </div>
      </div>
  </div>
</template>

<script>
import Search from './components/Search.vue'
import Card from './components/Card.vue'

export default {
    name: 'App',
    components: {
        Search,Card
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
