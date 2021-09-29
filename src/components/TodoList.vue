<template>
    <div>
        <ul>
            <TodoItem
            v-for="t of todosSimple"
            v-bind:todoForItem="t"
            v-on:remove-todo="deleteTodo"
            />
        </ul>
    </div>
</template>

<script>
import TodoItem from '@/components/TodoItem'
export default {
    props: ['todosSimple'],
    components: {
        TodoItem
    }, 
    methods: {
        deleteTodo(id) {
            this.$emit('remove-todo', id);
        }
    }
}
</script>

<style scoped>
    ul {
        list-stylle: none;
        margin: 0;
        padding: 0;
    }
</style>