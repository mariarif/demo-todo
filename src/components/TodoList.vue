<script setup>
import TodoListItem from './TodoListItem.vue';

const response = await fetch('https://jsonplaceholder.typicode.com/todos');
const todos = await response.json();
</script>

<template>
    <div class="div-item" >
        <TodoListItem
            v-for="todo of todos"
            :key="todo.id"
            :userId="todo.userId"
            :id="todo.id"
            :title="todo.title"
            :completed="todo.completed"
        />
    </div>
</template>

<style scoped>
.div-item{
    border: 4px dotted rgb(18, 61, 9) ;
    margin: 20px;
    padding: 15px;
    display: grid;
    grid-template-columns: 10% 70% 20%;
    background-color: rgb(148, 187, 140);
}
</style>