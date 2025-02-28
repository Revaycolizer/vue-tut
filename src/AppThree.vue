<script setup>
import { ref, onMounted } from 'vue';

const name = ref('Vue Jobs');
const status = ref('active'); // active, pending, inactive
const tasks = ref([]);
const newTask = ref('');

const link = 'https://cpage.co.tz';
const link2 = 'https://google.com';

const toggleStatus = () => {
    if (status.value === 'active') {
        status.value = 'pending';
    } else if (status.value === 'pending') {
        status.value = 'inactive';
    } else {
        status.value = 'active';
    }
}

const addTask = () => {
    if (newTask.value.trim() !== '') {
        tasks.value.push(newTask.value);
        newTask.value = '';
    }
}

const deleteTask = (index) => {
    tasks.value.splice(index, 1);
}


onMounted(async () => {
    try {
        const response = await fetch('https://jsonplaceholder.typicode.com/todos');

        if (!response.ok) {
            throw new Error('Failed to fetch data');
        } else {
            const data = await response.json();
            tasks.value = data.map((task) => task.title);
        }
    } catch (error) {
        console.log(error);
    }

})
</script>

<template>
    <h1>{{ name }}</h1>

    <p v-if="status === 'active'">User is active!</p>
    <p v-else-if="status === 'pending'">User is pending!</p>
    <p v-else>User is inactive!</p>

    <h3>Tasks</h3>
    <form @submit.prevent="addTask">
        <label for="newTask">Add Task</label>
        <input type="text" id="newTask" name="newTask" placeholder="Add Task" v-model="newTask">
        <button type="submit">Add Task</button>
    </form>
    <ul>
        <li v-for="(task, index) in tasks" :key="task">
            <span>{{ task }}</span>
            <button @click="deleteTask(index)">x</button>
        </li>
    </ul>

    <a v-bind:href="link">Click for cPage</a>
    <a :href="link2">Click for Google</a>
    <br>
    <button v-on:click="toggleStatus">Change Status</button>



</template>





<style scoped>
h1 {
    color: red;
}
</style>
