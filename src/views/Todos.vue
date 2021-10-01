<template>
  <div>
        <h2>Todo application</h2>
        <router-link to="/">Home</router-link>
        <hr>
        <AddTodo 
         @add-todo="addTodo"
        />
        <select v-model="filter">
            <option value="all">All</option>
            <option value="completed">Completed</option>
            <option value="not-completed">Not-completed</option>
        </select>
        <Loader v-if="loading"/>
        <!-- До computed было todo -->
        <TodoList
          v-else-if="filteredTodos.length"  
         v-bind:todosSimple="filteredTodos"
         @remove-todo = "removeTd"
        /> <!-- вместо v-on -->

        <p v-else>No todos!</p>
     </div>
</template>

<script>
import TodoList from '@/components/TodoList.vue';
import AddTodo from '@/components/AddTodo.vue';
import Loader from '@/components/Loader.vue';
export default {
    name: 'App',
    data() {
        return {
            todos: [
                //  {id:1, title: 'Купить хлеб', completed: false},
                //  {id:2, title: 'Купить молоко', completed: false},
                //  {id:3, title: 'Купить масло', completed: false}
            ],
            loading: true,
            filter: "all"
        }
    },
    mounted() {
        fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
            .then(response => response.json())
            .then(json => {
                setTimeout(() => {
                    this.todos = json
                    this.loading = false
                }, 0)

            })
    },
    // watch: {
    //     filter(value) {
    //         console.log(value)
    //     }
    // },
    computed: {
        filteredTodos() {  // Работает как переменная
            if (this.filter === 'all') {
                return this.todos
            }

            if (this.filter === 'completed') {
                return this.todos.filter(t => t.completed)
            }

            if (this.filter === 'not-completed') {
                return this.todos.filter(t => !t.completed)
            }
        }
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
        AddTodo,
        Loader
    }
}
</script>
