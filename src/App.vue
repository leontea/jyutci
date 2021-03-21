<template>
  <div id="app">
    <word-search />

  </div>
</template>

<script>
import WordSearch from './components/WordSearch.vue'

export default {
  name: 'App',
  data(){
    return{
      comName:"WordSearch"
    }
  },
  components: {
    WordSearch
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

@import'~bootstrap/dist/css/bootstrap.css';



</style>
