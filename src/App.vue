<template>
  <div id="app">
    <Champion />
    <Level />
    <br>
    <Drake />
  </div>
</template>

<script>
import axios from 'axios'

import Level from './components/Level.vue'
import Drake from './components/Drake.vue'
import Champion from './components/Champion.vue'


export default {
  name: 'app',
  components: {
    Level,
    Drake,
    Champion
  }
}
</script>

<style>
#app {
  
}
</style>
