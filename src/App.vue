<template>
  <div class="app">
    <app-header></app-header>
    <router-view/>
  </div>
</template>

<script>

import Header from './components/Header.vue'
export default {
  name: 'App',
  components: {
    'app-header': Header
  },
  data (){
    return {
      title: 'Vue Application'
    }
  },
}
</script>

<style>
body{
  padding: 0;
  margin:0;
}
.app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /*text-align: center;*/
  color: #2c3e50;
}
</style>
