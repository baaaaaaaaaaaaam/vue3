<template>
    <br>
    {{msg}}
    <br>
    parent  : {{ParentText}}
    <br>
    <Child v-model:childText="ParentText"></Child>
</template>

<script>
import Child from './EmitChild.vue'
import { ref, watch } from 'vue'

export default {
    components:{
        Child
    },
    setup(props,context) {
        const ParentText = ref('input');
        const msg = context.attrs.msg;
        watch(
            ParentText,()=>{
                console.log('watch')
            }
        )
        return {
            msg,ParentText
        }
    },
}
</script>
<style>

</style>