<template>
  <div class="container">
    <div class="header">
      <h1>Todo App v1</h1>
      <TodoInput :todos="todos" @submitTodo="addTodo"/>
    </div>
    <div v-if="loading===2" class="todo-container">
      <template v-for="todo in todos" :key="todo.id">
        <TodoItem :todo="todo" @toggle="toggleCompleted" @remove="removeTodo"/>
      </template>
    </div>
    <div v-if="loading===3" class="todo-container">
      <h2>No todo found</h2>
      <p>Please add one todo above...</p>
    </div>
  </div>
</template>

<script>
import {todos} from '../utils/dummyTodos'
import TodoItem from './TodoItem.vue'
import TodoInput from './TodoInput.vue'

export default {
  components:{TodoItem, TodoInput},
  data(){
    return{
      todos:[],
      loading:1
    }
  },
  created(){
    const sortedTodos = todos.sort((t1,t2)=>t2.id - t1.id)
    if(sortedTodos.length!==0) {
      this.loading = 2
      this.todos = [...sortedTodos]
    }
    if(sortedTodos.length===0) this.loading = 3
  },
  updated(){
    if(this.todos.length===0)  this.loading = 3
    if(this.todos.length!==0)  this.loading = 2
  },
  methods:{
    toggleCompleted(todo){
      const findTodo = this.todos.find((t)=>t.id === todo.id)
      findTodo.isCompleted = !findTodo.isCompleted
      const updatedTodos = this.todos.filter((t)=>t.id !== todo.id)
      updatedTodos.push(findTodo)
      const sortedTodos = updatedTodos.sort((t1,t2)=>t2.id - t1.id)
      this.todos = sortedTodos
    },
    addTodo(todo){
      const todos = [...this.todos]
      todos.push(todo)
      const sortedTodos = todos.sort((t1,t2)=>t2.id - t1.id)
      this.todos = sortedTodos
    },
    removeTodo(todo){
      const todos = [...this.todos]
      const removedTodo = todos.filter((t)=>t.id!==todo.id)
      const sortedTodos = removedTodo.sort((t1,t2)=>t2.id - t1.id)
      this.todos = sortedTodos
    }
  }
}
</script>

<style scoped>
  .container{
    max-width: 500px;
    margin: 0px auto;
    padding: 0px 24px;
  }
  .todo-container{
    display: flex;
    flex-direction: column;
    width: 100%;
    justify-content: center;
    align-items: center;
  }
  .header{
    position: sticky;
    top: 0px;
    background: white;
    padding: 60px 0px 12px 0px;
    box-sizing: border-box;
  }
  .header h1{
    margin-bottom: 24px;
  }
</style>