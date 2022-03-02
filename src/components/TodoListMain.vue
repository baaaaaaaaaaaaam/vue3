<template>
    <!-- 작업 리스트 선택 및 필터 부분 -->
  <todo-list-menu @change-filter="onChangeFilter" class="p-0"/>
    <!-- 선택한 작업 리스트 표시 -->
   <div v-for="key in Object.keys(filtered_todos)" :key="key" class="mb-3">
       <div v-if="use_category">
           <em>{{key}}</em>
       </div>
       <todo-list :data="filtered_todos[key]" />
   </div>
   <!-- 처리 기한이 넘은 작업 리스트 -->
   <div class="my-2 mt-5">
       <span style="background-color: red">&nbsp;</span>&nbsp;
       <strong>처리기한이 넘은 작업들</strong>
   </div>
   <todo-list :data="pending_todos"></todo-list>
</template>

<script>
import TodoList from "./TodoList.vue";
import {ref,provide,inject,watch} from 'vue'
import {useFilter} from '../compositions/useFilter'
import TodoListMenu from './TodoListMenu.vue'
export default {
    components:{
        TodoList,TodoListMenu
    },
    name: 'TodoListMain',
    setup(props){
        const{
            getPendingTodos,
            getActiveTodayTodos,
            getCompletedTodayTodos,
            getAllTodayTodos,
            getAllTodos
        } = useFilter()
        const filter = ref(0)   //  작업 메뉴 에서 선택한 value 
        const filtered_todos = ref([]) // 메뉴에 맞기 분류한 todos를 날짜별로 그룹화 진행
        const pending_todos = ref([])   // 처리하지 못한 데이터들
        const use_category = ref(false); // 모든 작업인 경우에만 true , 화면에서 그룹화된 날짜를 표시함
        const todos = inject('todos')  // 전체 리스트 
        //TodoListMenu에서 드랍버튼 사용시 불러옴
        const filters = {
            0:{
                str:'해야 할 작업들',
                func: getActiveTodayTodos,
                category: false 
            },
            1:{
                str:'완료 한 작업들',
                func: getCompletedTodayTodos,
                category: false 
            },
            2:{
                str:'오늘의 모든 기록',
                func: getAllTodayTodos,
                category: false 
            },
            3:{
                str:'모든작업',
                func: getAllTodos,
                category: true 
            },
        }
        provide('filters',filters);


        const groupBy = (todos) =>{  // reduce 함수를 사용하여 날짜별로 데이터를 그룹핑함
            return todos.reduce((acc,cur)=>{
                acc[cur['date']]= acc[cur['date']]||[];
                acc[cur['date']].push(cur)
                return acc
            },{})
        }
        //TodoListMenu 에서  필터를 변경할때마다 emit으로 호출됨
        // onChangeFilter  가 호출되면 watch도 호출됨  
        const onChangeFilter = (filter_idx)=>{
            console.log(filter_idx)
            filter.value =Number(filter_idx);
        }
        
        //여기서 watch 는 TodoListMenu의 필터를 변화하거나 or todos 리스트의 변화를 감지하는 역활을 한다
        /*
            watch 첫 인수에는 source ( ref 는 아래처럼 ,reactive 는 ()=> 형태로 사용)
            두번째 인수에는 new ,old 인자가 들어간다.
            watch를 사용하여 두가지 변수를 한번에 감시하려면 아래와같이 첫번쨰 인자에 ([a,b]) 를 추가한다
            두번쨰 인자에도 ([],[]) 아래형태를 사용한다.
        */
        watch ([filter,todos],([newValueFilter,newValueTodos],[oldValueFilter,oldValueTodos])=>{
            console.log(newValueFilter)
            console.log(newValueTodos)
            console.log(oldValueFilter)
            console.log(oldValueTodos)
            pending_todos.value=getPendingTodos(todos) //처리기한 넘은 리스트   
            let tmp_todos = filters[newValueFilter].func(todos);  //작업 메뉴 선택시 todos 를 메뉴에 맞게 분류 
            console.log(tmp_todos)
            filtered_todos.value =groupBy(tmp_todos);  // 메뉴에 맞기 분류한 todos를 날짜별로 그룹화 진행
            console.log(filtered_todos)
            use_category.value= filters[newValueFilter].category;  // 모든 작업인 경우에만 true , 화면에서 그룹화된 날짜를 표시함
        },{immediate:true})     // undefined -> init 값으로 변경됨을 감지하는지 확인

     
        return {
            filter,
            pending_todos,
            filtered_todos,
            use_category,
            onChangeFilter
        }
    }
}
</script>

<style>

</style>