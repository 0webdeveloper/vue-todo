<template>
  <div>
        <h2>Todo application</h2>
        <router-link to="/">Home</router-link>
        <hr>
        <AddTodo 
         @add-todo="addTodo"/>
        <TodoList v-bind:todosSimple="todos"
         @remove-todo = "removeTd"/> <!-- вместо v-on -->
     </div>
</template>

<script>
import TodoList from '@/components/TodoList.vue';
import AddTodo from '@/components/AddTodo.vue';
export default {
    name: 'App',
    data() {
        return {
            todos: [
                //  {id:1, title: 'Купить хлеб', completed: false},
                //  {id:2, title: 'Купить молоко', completed: false},
                //  {id:3, title: 'Купить масло', completed: false}
            ]
        }
    },
    mounted() {
        fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
            .then(response => response.json())
            .then(json => {
                this.todos = json
            })
    },
    methods: {
        removeTd(id) {
            this.todos = this.todos.filter(t => t.id !== id);
        },
        addTodo(todo) {
            this.todos.push(todo);
        }
    },
    components: {
        TodoList,
        AddTodo
    }
}
</script>
