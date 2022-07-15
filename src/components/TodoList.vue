<script setup>
import TodoListItem from './TodoListItem.vue';
import {ref, reactive, toRefs, watch} from 'vue';

const response = await fetch('https://jsonplaceholder.typicode.com/todos');
let todos = await response.json();
todos=todos.slice(0,10);
const reactiveTodos=ref(todos);

const counter= reactive({
    deleted: 0,
    updated: 0
   
});

function getUpdatedCounter(){
    return counter.updated;
}

watch(() => counter.updated, (newValue, oldValue) => {
    console.log(`Counter updated ${oldValue} -> ${newValue}`);
});


//
// const counter=ref(0);
// watch(counter, (newValue,oldValue)=> {
//     console.log(`Counter ${oldValue} to ${newvalue}`);
// }) //2: functie ce se apeleaza



// const counter2=reactive({
//     ...toRefs(counter),
//     total: 0
// });

function handleTodoItemDeleted(todoItemId){
     reactiveTodos.value=reactiveTodos.value.filter(item => item.id !== todoItemId);
    counter.deleted++;
 }

function handleTodoItemCompleted(todoItemId, completed){
         reactiveTodos.value=reactiveTodos.value.map(todo=>{
        if(todo.id===todoItemId){
            return{
                ...todo,
                completed: completed
            };
        }
        else{
                return todo;
        }
        
    });
        
        console.log(`item completed: ${todoItemId} >> ${completed}`);
        counter.updated++;
 }

const newTodoTitle=ref("");
// watch(newTodoTitle, null => {
//     consolele.log(`checkbox: ${newValue}`);
// })


function handleAddNewTodoItem(){
    let newTodo={};
    newTodo.id=20;
    newTodo.title=newTodoTitle.value;
    newTodo.completed=false;
    reactiveTodos.value.push(newTodo);
}

const checkbox=ref(true);

watch(checkbox, newValue => {
    consolele.log(`checkbox: ${newValue}`);
});

const isDisabled=ref(true);

watch(()=> newTodoTitle.value, (newValue) => {
if(newValue.length===0)
    isDisabled.value= true;
    else isDisabled.value= false;
}
    );


</script>

<template>
    <section class="form">
        <div class="field">
            <label class="label">Todo:</label>
            <div class="input">
                <input v-model="newTodoTitle" type="text" class="inputTitle" />
            </div>
            <button class="btnAdd" :disabled="isDisabled" @click="handleAddNewTodoItem()" placeholder="..todo.." >Add new Todo</button>
        </div>
    </section>
    <span>Two-way data binding (v-model):</span>
    <input type="checkbox" v-model="checkbox" />
    <h3>Changes [deleted: {{counter.deleted}}, updated: {{counter.updated}}] </h3>
    <div class="todo-list" >
        
        <TodoListItem
            v-for="todo of reactiveTodos"
            :key="todo.id"
            :userId="todo.userId"
            :id="todo.id"
            :title="todo.title"
            :completed="todo.completed"
            @todo-item-deleted="handleTodoItemDeleted(todo.id)"
            @todo-item-completed="completed => handleTodoItemCompleted(todo.id, completed)"
            
        />
    </div>
</template>

<style scoped>
.todo-list{
    border: 4px dotted rgb(18, 61, 9) ;
    margin: 20px;
    padding: 15px;
    display: grid;
    grid-template-columns: 10% 70% 20%;
    background-color: rgb(148, 187, 140);
}
.field{
    display:grid;
    grid-template-columns:100px 300px 100px;
}
.input{
    width: 500px;
}
</style>