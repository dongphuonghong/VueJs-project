<template>
<img alt="Vue logo" src="./assets/logo.png">
<bt1></bt1>
<HelloWorld msg="Welcome to Your Vue.js App"/>
<bai2></bai2>
<bt3></bt3>
</template>

<script>
import bai2 from './components/bai2.vue'
import bt1 from './components/bt1.vue'
import HelloWorld from './components/HelloWorld.vue'
import bt3 from './components/bt3.vue'
export default {
name: 'App',
components: {
bai2,
bt1,
HelloWorld,
bt3
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