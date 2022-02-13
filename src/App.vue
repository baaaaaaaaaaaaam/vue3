<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <!-- <LifeCycle msg="Welcome to Your Vue.js App"/> -->
  <!-- <Vmodel msg="Welcome to Your Vue.js App"/> -->
  <!-- <Reactive msg="Welcome to Your Vue.js App"/> -->
  <!-- <Computed msg="Welcome to Your Vue.js App"/> -->
  <!-- <Watch msg="Welcome to Your Vue.js App"/> -->
  <Props msg="Welcome to Your Vue.js App" :data="[1,2,3]"/>

</template>

<script setup>
// import LifeCycle from './components/LifeCycle.vue'
// import Vmodel from './components/Vmodel.vue'
// import Reactive from './components/Reactive.vue'
// import Computed from './components/Computed.vue'
// import Watch from './components/Watch.vue'
import Props from './components/Props.vue'
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
