<script lang="ts">
import Header from './Header.vue';
import Todo from './Todo.vue';


    export default {
        name: 'CardVue',
        components: {
            Header,
            Todo
        }
    }

</script>

<template>
    <div class=" w-[28rem] h-[45rem] rounded-2xl border-4 border-t-purple-600 border-r-pink-600 border-b-pink-600 border-l-indigo-600  bg-gradient-to-r from-indigo-500 via-purple-500 to-pink-500 shadow-md shadow-white font-sans">
        <Header/>
        <Todo/>
    </div>

</template>