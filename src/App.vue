<template>
  <div id="app">
        <h1>Todo application</h1>
        <TodoList v-bind:todosSimple="todos"
         @remove-todo = "removeTd"/> <!-- вместо v-on -->
     </div>
</template>

<script>
import TodoList from '@/components/TodoList.vue';
export default {
  name: 'App',
  data() {
    return {
     todos: [
       {id:1, title: 'Купить хлеб', completed: false},
       {id:2, title: 'Купить молоко', completed: false},
       {id:3, title: 'Купить масло', completed: false}
     ] 
    }
  },
    methods: {
    removeTd(id) {
      this.todos = this.todos.filter(t => t.id !== id);
      console.log(this.todos);
    }
  },
  components: {
   TodoList
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
