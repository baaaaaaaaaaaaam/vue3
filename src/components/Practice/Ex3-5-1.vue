<template>
    <label> 이름 : </label>  
    <input type="text" v-model="result.name" placeholder="이름"> <br>
    <label> 나이 : </label>  
    <input type="text" v-model="result.age" placeholder="나이"> <br>
    <label> 성별 : </label>  
    <label> 남성 </label>  
    <input type="radio" name="gender"  v-model="result.gender" value="male"> 
    <label> 여성 : </label>  
    <input type="radio" name="gender"  v-model="result.gender" value="female"> <br>
    <label> 취미 : </label>  
    <span v-for="(hobby,key) in hobby_options" :key="key">
        <label>{{hobby}}</label>
        <input type="checkbox" v-model="result.hobby" :value="hobby">
    </span>
    <br>
    <label> 비번 : </label>  
    <input type="password" v-model="result.password"> <br>
    <label> 국가 : </label>  
    <select v-model="result.country">
        <option v-for="(country,key) in country_options" :key="key">
            {{country}}
        </option>
    </select>
    <br>
    <input type="date" v-model="result.data">
    <br>
    <input type="time" v-model="result.time">
    <br>
    <input type="color" v-model="result.color">
    <br>
    <input type="range" min="1" max="100" v-model="result.range">

    <div>
        <h3>결과</h3>
        <hr>
        {{result}}
    </div>

</template>
<script>
import {reactive} from 'vue'
export default {
    setup() {
        let name = '';
        let age =0;
        let gender ='male';
        let hobby=['스포츠'];
        let password = '';
        let country='한국';
        let date='';
        let time='';
        let color='';
        let range=0;
        let country_options = ['한국','미국','중국'];
        let hobby_options = ['스포츠','그림','음악','코딩'];
        let result=reactive({name,age,gender,hobby,password,country,date,time,color,range})
        return{
            result,
            country_options,
            hobby_options
        }
    },
}
</script>

<style scoped>

</style>