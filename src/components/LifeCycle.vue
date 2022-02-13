<template>
  <p>{{$attrs.msg}}</p>
  <p>{{count}}</p>
  <button @click="count++">+++</button>
  <button @click="count--">---</button>
</template>

<script>
import { ref,onUpdated, onBeforeMount, onMounted, onBeforeUpdate, onBeforeUnmount,onUnmounted ,onRenderTracked ,onRenderTriggered} from 'vue'

export default {
  setup(){
    const count = ref(0)
    onBeforeMount(()=>{
      console.log('onBeforeMount',count.value)
    });
    onMounted(()=>{
      console.log('onMounted',count.value)
    })
    onBeforeUpdate(()=>{
       console.log('onBeforeUpdate',count.value)
    })
    onUpdated(()=>{
      console.log('onUpdated',count.value)
    })
    onBeforeUnmount(()=>{
      console.log('onBeforeUnmount',count.value)
    })
    onUnmounted(()=>{
      console.log('onUnmounted',count.value)
    })
    onRenderTracked((e)=>{
      console.log('onRenderTracked',count.value,e.target)
    })
    onRenderTriggered(()=>{
      console.log('onRenderTriggered',count.value)
    })
    return {
      count
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
