<template>
  <p>{{$attrs.msg}}</p>
  <p>{{count}}</p>
  <input type="text" v-model.lazy="count">
  <input type="text" v-model.number="count">
  <input type="text" v-model.trim="count">

</template>

<script>
import { ref,onUpdated} from 'vue'

export default {
  setup(){
    const count = ref(0)
    onUpdated(()=>{
      console.log('onUpdated',count.value)
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
