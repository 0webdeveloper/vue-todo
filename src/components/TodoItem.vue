<template>
    <li>
        <span v-bind:class="{done: todoForItem.completed}">
            <input type="checkbox" v-on:change="todoForItem.completed = !todoForItem.completed">
            <strong>{{index + 1}}</strong>
            {{todoForItem.title}}
        </span>
        <button class="remove" v-on:click="$emit('remove-todo', todoForItem.id)">&times;</button>
    </li>
</template>

<script>
    export default {
        props:{
            todoForItem: {
                type: Object,
                requred: true
            },
            index: Number
        }
    }
</script>

<style scoped>
    li {
        border: 1px solid #ccc;
        display: flex;
        justify-content: space-between;
        padding: .5rem 2rem;
        margin-bottom: 1rem;
    }
    input{
        margin-right: 1rem;
    }
    .remove{
        background: #cc0000;
        color: #fff;
        border-radius: 50%;
        border: none;
        display: flex;
        /* align-items:center; */
        justify-content: center;
        font-size: 18px;
        width: 20px;
        height: 20px;
    }
    .done {
        text-decoration: line-through;
    }
</style>