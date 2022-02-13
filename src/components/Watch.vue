<template>
    <p>{{human}}</p>
    <button @click="onClicked1"> 버튼</button>
    <hr>
    <div v-for="(monster , key ) in humans" :key="key">
        <p>{{monster}}</p>
    </div>
    <button @click="onClicked2"> 이탁구 -> 소탁구</button>
</template>
<script>
import {reactive, ref , watch} from 'vue'

export default {
    setup() {
        const human = ref('늑대인간');
        const humans = reactive([{name:'김탁구',id:1},{name:'이탁구',id:2},{name:'차탁구',id:3},{name:'북탁구',id:4}])
        const onClicked1 = () => {
            human.value='초록인간'
        }
        const onClicked2 = () => {
            humans[1].name='소탁구'
        }
        watch(
            human,
            (cur,prev)=>{
                console.log(`human watch prev ${prev} => cur ${cur}`)
            },
            {
                immediate:true
            }
        )
         watch(
            humans,
            ()=>{
                console.log(`humans watch !!!!!!!!!!!!`)
            },
            {
                immediate:false
            }
        )
        return{
            human,onClicked1,humans,onClicked2
        }
    },
}
</script>

<style scoped>

</style>