<template>
  <header>
    <hgroup class="my-5">
      <h1>나의 할일</h1>
      <em>{{today}}</em>
    </hgroup>
  </header>
  <TodoListContainer/>
</template>

<script>
import { inject  } from 'vue'
import TodoListContainer from './components/TodoListContainer.vue'


export default {
  components:{
    TodoListContainer
  },
  name:'App',
  setup(){
    const today = inject('today');

    return{
      today
    }
  }
}

</script>

<style scoped>

hgroup {
  text-align: center;
  font-family: 'Arial Bold';
}
hgroup h1 {
  font-weight: bolder;
}
</style>
