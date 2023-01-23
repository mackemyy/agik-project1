<script setup >
import { ref } from 'vue';
    const todoName = ref("");
    const todos = ref([]);
    const addTodo = () => { 
        if(!todoName.value) {
            alert("Please provide a task.")
        } else {
            const todo = {
            id: Date.now().toString(),
            todo: todoName.value,
            };
            todos.value.push(todo);
            todoName.value = "";
        }
    };

    const deleteTodo = (id) => {
        const newTodo = todos.value.filter((item) => item.id !== id);
        todos.value = newTodo;
    }

    const deleteAllTodo = () => {
        if(todos.value === []) {
            alert("Todo list is empty!");
        } else {
            todos.value=[];
        }
        
    }

</script>

<template>
    <div class="">
        <div class="m-8 ">
            <input type="text" class="w-[100%] pt-[10px] pr-[15px] font-sans block rounded-lg h-10 mb-[0.5rem] text-sm p-3" v-model="todoName" v-on:keyup.enter="addTodo" placeholder="Enter Your Task">
            <button class="px-6 py-2 bg-white rounded-lg text-sm cursor-pointer hover:bg-blue-900 hover:text-white flex justify-end whitespace-nowrap mr-3 ml-[16.5rem]" @click="addTodo">Add Task</button>
        </div>
        <div class="h-[22rem] overflow-auto">
            <p class="font-sans text-white text-xl pl-[30px] mb-4">ALL TASKS</p>
            <div class="todos mx-[3rem]">
                <ul class=" mb-3 ">
                    <li v-for="(todo, index) in todos" :key="index" class="list-none mb-2 text-white flex overflow-auto">
                        <span class="text-[12px] ">{{ todo.todo }}</span>
                        <button @click="()=> deleteTodo(todo.id)" class="px-5 py-[5px] text-white bg-red-600 text-[11px] rounded-lg text-center whitespace-nowrap cursor-pointer hover:bg-white hover:text-red-600">Delete Task</button>
                    </li>
                </ul>
            </div>
            
        </div>
        <div class="mt-5 flex justify-center w-full">
                <buttton class="px-6 py-2 text-white bg-red-600 text-sm rounded-lg text-center whitespace-nowrap relative right-0 bottom-0 cursor-pointer hover:bg-white hover:text-red-600" @click="deleteAllTodo">Delete All</buttton>
        </div>
    </div>
</template>

<style>
.todos ul li {
    
    display: flex;
    justify-content: space-between;
}
</style>
