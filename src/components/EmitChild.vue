<template>
     
    <input v-model="childText" @input="$emit('update:childText',$event.target.value)"> 
    <br>
    child : {{childText}}
</template>

<script>
import { ref } from 'vue'

export default {
    emits:['update:childText'],
    setup(props,context) {
         const childText = ref(context.attrs.childText);
     
         return{
             childText 
         }
    },
}
</script>
<style>

</style>