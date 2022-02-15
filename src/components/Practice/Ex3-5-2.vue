<template>
    <button v-bind="$attrs" :type="type" :class="classes" ref="button" @click="$emit('update:active',!active1);onClicked()">  
        <slot></slot>    
    </button>    
</template>
<script>
import {ref,onMounted, watch } from 'vue'

export default {
    props:{
        type:{
            default: 'button',
            validator:(value)=>{
                const allowed=['button','submit','reset','switch']
                return allowed.includes(value)
            },
        },
        sm: Boolean,
        md: {
            type:Boolean,
            default:true
        },
        lg: Boolean,
        pill: Boolean
    },
    emits:['update:active'],
    setup(props,context) {
        const classes=[];
        const button =  ref(null); 
        const active1 = ref(context.attrs.active);
        if(props.sm) classes.push('sm');
        else if(props.lg) classes.push('lg');
        else classes.push('md');
        if (props.pill) classes.push('pill');

        const onClicked = () =>{
            console.log('123')
            active1.value=!active1.value
        }
         
        //mounted 훅
        onMounted(()=>{
            Object.keys(context.attrs).forEach((attr)=>{
                if(attr.startsWith('text-')) button.value.style.color = attr.substring(5);
                if(attr.startsWith('background-')) button.value.style.backgroundColor = attr.substring(11);
            })
        })
        watch(context.attrs.active,()=>{
            console.log('t1')
        })
        return{
            classes,
            button,
            active1,
            onClicked
        }
    },
}
</script>
<style scoped>
    button{
        outline: none;
    }
    .sm{
        height: 20px;
        font-size: 13px;
    }
    .md{
        height: 30px;
        font-size: 22px;
    }
    .lg{
        height: 40px;
        font-size: 31px;
    }
    .pill{
        border-radius: 16px;
    }
    .deactive{
        filter: brightness(50%);
    }
</style>