<template>
  <div class="card" :class="{completed: todo.isCompleted}" @click="handleClick">
    <!-- <i v-if="todo.isPriority" class="bi bi-star-fill"></i>
    <i v-if="!todo.isPriority" class="bi bi-star"></i> -->
    <p>{{todo.name}}</p>
    <i class="bi bi-x-square" @click="handleRemove"></i>
  </div>
</template>

<script>
export default {
  props: ['todo'],
  methods:{
    handleClick(){
      this.$emit('toggle', this.todo)
    },
    handleRemove(){
      this.$emit('remove', this.todo)
    }
  }
}
</script>

<style scoped>
  .card{
    box-sizing: border-box;
    border: 1px solid rgba(124,188,255, 1);
    background: rgba(124,188,255, 0.2);
    margin: 16px 0px;
    width: 100%;
    border-radius: 0.5rem;
    cursor: pointer;
    transition: all 0.2s ease-in-out;
    display: flex;
    flex: row;
    align-items: center;
    padding: 24px;
  }
  .card p, .card i{
    font-size: 1.6rem;
    color: rgba(124,188,255, 1);
    margin: 0;
    text-transform: capitalize;
  }

  .card p {
    text-align: center;
    width: 100%;
  }

  .card:hover{
    background: rgba(124,188,255, 1);
    color: white;
    box-shadow: 0px 5px 9px 5px rgba(0,0,0,0.2);
    -webkit-box-shadow: 0px 5px 9px 5px rgba(0,0,0,0.2);
    -moz-box-shadow: 0px 5px 9px 5px rgba(0,0,0,0.2);
  }

  .card:hover i, .card:hover p{
    color: white;
  }

  .completed{
    background: #eee;
    border: 1px #aaa solid;
  }
  .completed p {
    text-decoration: line-through;
  }
  .completed.card p, .completed.card i{
    font-size: 1.6rem;
    color: #aaa;
    margin: 0;
    text-transform: capitalize;
  }

  .completed:hover{
    background: #eee;
    border: 1px #aaa solid;
    box-shadow: none;
  }

  .completed:hover i, .completed:hover p{
    color: #aaa;
  }

  .card i:hover{
    color: red;
  }
</style>