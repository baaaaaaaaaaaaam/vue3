<template>
   <div class="row">
       <div class="col">
           <span style="background-color: blue">&nbsp;</span>
           <strong>{{state}}</strong>
           <span style="background-color: blue">&nbsp;</span>
       </div>
       <div class="col">
           <div class="btn-group dropdown-toggle">
               <button class="btn btn-sm dropdown-toggle" type="button" data-bs-toggle="dropdown">
                필터
               </button>
               <ul class="dropdown-menu dropdown-menu-end">
                   <li v-for="(item,index) in filters" :key="index">
                       <a class="dropdown-item" @click="filter = (index)">
                           {{item.str }}
                       </a>
                   </li>
               </ul>
           </div>
       </div>
   </div>
</template>

<script>
import { ref,watch,computed,inject } from 'vue'

export default {
    name: 'TodoListMenu',
    emits:['change-filter'],
    setup(props,context){
        const filters= inject('filters')
        const filter =ref(0)
        const state = computed(()=>{
            return filters[filter.value].str
        })
        // 필터 드랍 박스에서 값을 선택하면 filter 값이 index로 변경됨으로써 watch를 호출하게함. 호출된 watch는 emit을 호출하여 
        // TodoListContainer 에 전달
        watch (filter,(newValue,oldValue)=>{
            console.log(newValue)
            console.log(oldValue)
            context.emit('change-filter',newValue)
        })
        return {
            state,filter,filters
        }
    }
}
</script>

<style>

</style>