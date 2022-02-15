<template>
  <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
  <!-- <LifeCycle msg="Welcome to Your Vue.js App"/> -->
  <!-- <Vmodel msg="Welcome to Your Vue.js App"/> -->
  <!-- <Reactive msg="Welcome to Your Vue.js App"/> -->
  <!-- <Computed msg="Welcome to Your Vue.js App"/> -->
  <!-- <Watch msg="Welcome to Your Vue.js App"/> -->
  <!-- <Props msg="Welcome to Your Vue.js App" :data="[1,2,3]"/> -->
  <!-- <EmitParent msg="Welcome to Your Vue.js App"/> -->
  <!-- <Ex1/> -->
  <!-- <MyButton sm> MyButton Test </MyButton>
  <MyButton lg> MyButton Test </MyButton>
  <MyButton pill> MyButton Test </MyButton>
  <MyButton background-white pill> MyButton Test </MyButton> -->
  <MyButton type="switch" v-model:active="active"> MyButton Test </MyButton>
  <!-- <MyButton type="switch" sep="2" v-model:active="active" @click="onClicked"> MyButton Test </MyButton> -->
</template>

<script>
// import LifeCycle from './components/LifeCycle.vue'
// import Vmodel from './components/Vmodel.vue'
// import Reactive from './components/Reactive.vue'
// import Computed from './components/Computed.vue'
// import Watch from './components/Watch.vue'
// import Props from './components/Props.vue'
// import EmitParent from './components/EmitParent.vue'
// import Ex1 from './components/Practice/Ex3-5-1.vue'
import {ref, watch} from 'vue'
import MyButton from './components/Practice/Ex3-5-2.vue'

export default {
  components:{
    MyButton
  },
  setup(){
    const active=ref(true)
    watch(active,()=>{
      console.log(active.value)
    })
    return {
      active,
    }
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
