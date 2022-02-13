<template>
    <p>{{$attrs.msg}}</p>
    <div v-for="(item,key) in arr1" :key="key">
        <p>{{`${key}-${item}`}}</p>
    </div>
    <hr>
    <div v-for="(item,key) in arr2" :key="key">
        <p>{{`${key}-${item}`}}</p>
    </div>
    <hr>
    <div v-for="(item,key) in arr3" :key="key">
        <p v-if="item.id == 2">{{`${key}-${item.id} ${item.name}`}}</p>
    </div>
    <hr>
</template>

<script>
import { reactive } from 'vue'

export default {
  setup(){
    const arr1 = reactive(['1번 배열','2번 배열','3번 배열','4번 배열'])
    const arr2 = reactive({1:'1번 obj',2:'2번 obj',3:'3번 obj',4:'4번 obj'})
    const arr3 = reactive([{id:'1',name:'김탁구'},{id:'2',name:'나탁구'},{id:'3',name:'배탁구'},{id:'4',name:'오탁구'},])
    return {
      arr1,arr2,arr3
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
