
<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to Your Vue.js App"/>  
  <bai_tap1></bai_tap1>
  <bai_Tap2></bai_Tap2>
</template>
<script>
import HelloWorld from './components/HelloWorld.vue'
import bai_tap1 from './components/bai_tap1.vue'

import bai_Tap2 from './components/bai_Tap2.vue'
export default {
  name: 'App',
  components: {
    HelloWorld,
    bai_tap1,
    bai_Tap2
    
    
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
