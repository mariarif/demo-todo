<script setup>
defineProps({
    userId: Number,
    id: Number,
    title: String,
    completed: Boolean
})
</script>

<template>
    <!-- <div class="grid-container">
        <div class="grid-line">    
            <input type="checkbox" :checked="completed" />
            {{ title }}
            <button>Delete</button>
        </div> 
    </div> -->

    <div class="grid-item">
        <input class="checkCompleted" type="checkbox" :checked="completed" />
    </div>
    <div class="grid-item">
        {{ title }}
    </div>
    <div class="grid-item">
        <button class="btnDelete">Delete</button>
    </div>

</template>

<style scoped>
/* .grid-container{
    display: grid;
    background-color: rgb(175, 216, 175);
    
}
.grid-line{
    margin: 10px;
    padding: 15px;
    display: inline-grid;
    background-color: rgb(222, 240, 212);
} */
.checkkCompleted{
    width: 30px;
}
.grid-item{
    border: 2px groove rgb(143, 160, 134) ;
    background-color: rgb(222, 240, 212);
    margin: 5px;
    padding: 10px;
}
.btnDelete{
    width: 100%;
    background-color: rgb(148, 187, 140);
}
</style>