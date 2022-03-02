<template>
  <todo-list-new />
  <section class="container">
    <div class="row justif-content-cneter m-2">
      <todo-list-main></todo-list-main>
    </div>
  </section>
</template>

<script>

import {ref,readonly,provide,onMounted} from 'vue'
import {useStorage} from '../compositions/storage';
import TodoListNew from './TodoListNew.vue';
import TodoListMain from './TodoListMain.vue'

export default {
  components:{
    TodoListNew,TodoListMain
  },
  name: 'TodoListContainer',
  setup(){
    const todos= ref([]);
    const { loadTodos,saveTodos,storage_id} = useStorage()

    //loadTodos 에서 LocalStorage 에 들어있는 데이터를 꺼내서 배열형태로 만들어서 todos에담음.
    const initTodos = () =>{
      todos.value = loadTodos();
      console.log(todos.value)
    }
    
    //TOdoListNew 에서 작업 추가를 누를경우 사용됨
    const addTodo = (job,date) => {
      todos.value.push({
        id:storage_id.value++,
        job:job,
        date:date,
        completed:false,
      })
      saveTodos(todos)
      initTodos()
    }
    
    //TodoList 에서 삭제 누를경우
    const removeTodo = (id) =>{
      //splice =  id 부터 1개 삭제 
      todos.value.splice(id,1)
      // todo.id 를 재정렬 
      todos.value.forEach((todo,idx)=>{
        todo.id=idx
      })
      //저장
      saveTodos(todos)
      //초기화 
      initTodos()
    }
    //TodoList 왼쪽 체크박스를 누르거나 할일 완료를 누를경우 
    const completeTodo = (id)=>{
      //find = 배열에서 가장 빠른 같은 값을 찾아낸다.
      todos.value.find((todo)=> todo.id == id).completed =true
      saveTodos(todos)
      initTodos()
    }
    provide('todos',readonly(todos))
    provide('addTodo',addTodo);
    provide('removeTodo',removeTodo);
    provide('completeTodo',completeTodo);
    //mounted 시점에 초기화 
    onMounted(()=>{
      initTodos();
    });

   
  }
}

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
