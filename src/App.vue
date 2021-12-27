<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="https://vuejs.org/images/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js App" /> -->

    <Key name="C" />
    <Key name="C#" />
    <Key name="D" />
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue';
import Key from './components/Key.vue';

export default {
  name: 'App',
  components: {
    HelloWorld,
    Key,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

div.app-key {
  width: 30px;
  height: 30px;
  border-color: black;
  border-style: solid;
  border-width: 0 1px 1px 1px;
}

div.app-key:first-child {
  border-width: 1px;
}
</style>
