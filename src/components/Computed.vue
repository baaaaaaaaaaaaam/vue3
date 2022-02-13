<template>
  <p>{{$attrs.msg}}</p>
  <p>{{count}}</p>
    <p>{{computed_count}}</p>

    <button @click="onClicked">button</button>
</template>

<script>
import { ref,onUpdated , computed ,onBeforeUpdate} from 'vue'

export default {
  setup(){
    const count = ref(0)
    const onClicked = () =>{
      console.log('method');
        count.value = 0;
    }
    onUpdated(()=>{
      console.log('onUpdated',count.value)
    })
     onBeforeUpdate(()=>{
       console.log('onBeforeUpdate',count.value)
    })
    const computed_count = computed(()=>{
        console.log('computed');
        return count.value;
    })
    return {
      count,onClicked,computed_count
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
