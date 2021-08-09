<template>
  <form @submit.prevent="handleSubmit">
    <input type="text" name="todo" placeholder="Add a new todo..." v-model="todo">
    <button>Add</button>
  </form>
</template>

<script>
export default {
  props:['todos'],
  data(){
    return{
      todo:''
    }
  },
  methods:{
    handleSubmit(){
      if(this.todos.find((t)=>t.name.toLowerCase().includes(this.todo.toLowerCase()))) return alert('The todo already exists!')
      const newTodo = {
        id: this.todos.length + 1,
        name: this.todo,
        isPriority:false,
        isCompleted:false
      }
      this.$emit('submitTodo',newTodo)
      this.todo = ''
    }
  }
}
</script>

<style scoped>
  form{
    width: 100%;
    margin-bottom: 12px;
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;
  }
  input{
    width: 70%;
    margin: auto;
    padding: 16px;
    font-size: 1.2rem;
    border-radius: 0.5rem;
    border: 1px solid rgba(124,188,255, 0.5);
  }

  input:focus-visible{
    outline: none;
    border-radius: 0.5rem;
    border: 2px solid rgba(124,188,255, 1);
  }

  button{
    width: 30%;
    margin-left: 20px;
    padding: 16px;
    border-radius: 0.5rem;
    background: rgba(124,188,255, 1);
    font-size: 1.2rem;
    border: none;
    color: white;
    cursor: pointer;
  }

  button:hover{
    background: rgb(94, 139, 187);
  }
</style>