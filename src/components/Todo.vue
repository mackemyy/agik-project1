<script setup >
import { ref } from 'vue';
import Dropdown from './Dropdown.vue';

    components: {
        Dropdown
    }

    const todoName = ref("");
    const todos = ref([]);
    const isCompleted = ref(false);
    const addTodo = () => { 
        const dateTime = new Date();
        const date = (dateTime.getMonth()+1)+'/'+dateTime.getDate()+'/'+dateTime.getFullYear();
        const time = dateTime.getHours() + ":" + dateTime.getMinutes();

        if(!todoName.value) {
            alert("Please provide a task.")
        } else {
            const todo = {
                id: Date.now().toString(),
                todo: todoName.value,
                isCompleted: isCompleted.value,
                timeCreated: time,
                dateCreated: date,
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

    const showAllTasks = () => {
        if(todos !== null) {
            const allTodos = todos.value;
            todos.value = allTodos;
        }
    }

    const showPendingTasks = () => {
        const pendings = todos.value.filter((item) => item.isCompleted !== true);
        todos.value = pendings;
    }

    const showCompletedTasks = () => {
        const completes = todos.value.filter((item) => item.isCompleted !== false);
        todos.value = completes;
    }

    const completeTask = (todo) => {
        return todo.isCompleted = !todo.isCompleted;
    }

</script>

<template>
    <div class="">
        <div class="m-8 ">
            <input type="text" class="w-[100%] pt-[10px] pr-[15px] font-sans block rounded-lg h-10 mb-[0.5rem] text-sm p-3" v-model="todoName" v-on:keyup.enter="addTodo" placeholder="Enter Your Task">
            <button class="px-6 py-2 bg-white rounded-lg text-sm cursor-pointer hover:bg-blue-900 hover:text-white flex justify-end whitespace-nowrap mr-3 ml-[16.5rem]" @click="addTodo">Add Task</button>
        </div>
        <div class="h-[22rem] overflow-auto">
            <!-- <p class="font-sans text-white text-xl pl-[30px] mb-4">ALL TASKS</p> -->
            <!-- <Dropdown/> -->
            <div class=" mb-4 mx-[30px] font-sans text-white text-[11px] flex justify-between items-center">
                <button @click="showAllTasks">ALL TASKS</button>
                <button @click="showPendingTasks">PENDING TASKS</button>
                <button @click="showCompletedTasks">COMPLETED TASKS</button>
            </div>
            <div class="todos mx-[2.5rem]">
                <ul class=" mb-3 ">
                    <li v-for="(todo, index) in todos" :key="index" :class="{ 'is-selected': todo.isCompleted }" class=" list-none mb-2 text-black flex overflow-auto justify-center bg-gray-100 p-[10px] rounded-lg">
                        <div>
                            <div class="flex items-center gap-2">
                                <input type="checkbox" id="todoCheck" v-on:click="() => completeTask(todo)" class="w-3 h-3 text-red-600 bg-gray-100 "/>
                                <label class="text-[12px]" for="todoCheck">{{ todo.todo }}</label>
                            </div>
                            <div class="flex justify-center items-center text-[10px] gap-1 pl-[1rem] ">
                                <div>{{ 'Date Created:   ' + todo.dateCreated }}</div>
                                <div>{{ 'at ' + todo.timeCreated }}</div>
                            </div>
                            
                        </div>
                        <button @click="()=> deleteTodo(todo.id)" class="px-4 text-white bg-red-600 text-[9px] rounded-lg text-center whitespace-nowrap cursor-pointer hover:bg-slate-900 hover:text-white">Delete Task</button>
                    </li>
                </ul>
            </div>
            
        </div>
        <div class="mt-5 flex justify-center w-full">
                <buttton @click="deleteAllTodo" class="px-6 py-2 text-white bg-red-600 text-sm rounded-lg text-center whitespace-nowrap relative right-0 bottom-0 cursor-pointer hover:bg-white hover:text-red-600">Delete All</buttton>
        </div>
    </div>
</template>

<style>
    .todos ul li {
        display: flex;
        justify-content: space-between;
    }

    .is-selected label {
        text-decoration: line-through;
        color: green;
    }
</style>
