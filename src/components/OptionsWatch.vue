<template>
    <div v-for="(monster , key ) in humans" :key="key">
        <p>{{monster}}</p>
    </div>
    <button @click="onClicked2"> 이탁구 -> 소탁구</button>
</template>
<script>


export default {
    data(){
        return {
            humans:[{name:'김탁구',id:1},{name:'이탁구',id:2},{name:'차탁구',id:3},{name:'북탁구',id:4}]
        }
    }
    ,methods:{
        onClicked2(){
            this.humans[1].name = '소탁구'
        }
    },
    watch:{
        humans:{
            deep: true,
            handler(humans){
                console.log(humans)
            }
        }
    }
}
</script>

<style scoped>

</style>