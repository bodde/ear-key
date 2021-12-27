<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="https://vuejs.org/images/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js App" /> -->
    <Keyboard />
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue';
import Keyboard from './components/Keyboard.vue';

export default {
  name: 'App',
  components: {
    HelloWorld,
    Keyboard,
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
