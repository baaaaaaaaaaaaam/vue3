<template>
    <br>

    {{msg}}
    {{data}}    
    
    <hr>
   
</template>

<script>
export default {

    setup(props,context) {
        const data = context.attrs.data
        const msg = context.attrs.msg
        return {
            data,msg
        }
    },
}
</script>

<style scoped>

</style>