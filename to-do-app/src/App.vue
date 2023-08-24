<script setup>
import { ref } from 'vue'; // Import ref from Vue 3

// Define reactive data properties
const newTask = ref('');
const tasks = ref([]);

// Function to add a new task
const addTask = () => {
  if (newTask.value.trim() !== '') {
    const task = { text: newTask.value, completed: false };
    tasks.value.push(task);
    newTask.value = ''; 
  }
};

// Function to remove a task by index
const removeTask = (index) => {
  tasks.value.splice(index, 1);
};

// Function to complete a task
const completeTask = (index) => {
  const task = tasks.value[index];
  if (task) {
    task.completed = true;
    completedTask.value.push(task);
    tasks.value.splice(index, 1);
  }
};

// Function to enable onPressEnter
const onPressEnter = (event) => {
  if (event.key === 'Enter') {
    addTask();
  }
};
</script>

<template>

  <div id="app">
        <h3>Tasks to-do:</h3>
        <div class="container">
            <input type="text" placeholder="New Task" v-model="newTask" @keydown.enter="onPressEnter"> 
            <button @click="addTask">+</button>
    </div>
    <br><br>

    <ul class="list">
        <li v-for="(task, index) in tasks" :key="index">
          <input type="checkbox" v-model="task.completed" />
          <span v-bind:class="task.completed?'completed':''">{{ task.text }}</span>
          <button @click="removeTask(index)">x</button>
        </li>
    </ul>
    </div>

</template>

<style>
body{
    margin: 0;
    padding: 0;
    background-color: #FDF5DF;
    font-family: 'Courier New', Courier, monospace;
}
</style>

<style scoped>

#app {
    position: absolute;
    height: 120px;
    left: 50%;
    top: 20%;
    transform: translate(-50%, -20%);
    padding: 6px 14px;
    background-color: white;
    box-shadow: 1px 1px 10px rgb(157, 156, 156);
    max-width: 500px;
}

h3{
    font-size: 32px;
    color: #FF6A3D;
}

.container {
   display: flex;
   flex-direction: row;
   flex-wrap: nowrap;
   justify-content: center;
   align-items: center; 
}

.container input[type="text"] {
    height: 40px;
    width: 100%;
    border: none;
    padding-left: 10px;
    font-size: 14px;
    transition: all .1s ease-in-out;
}

.container button {
    height: 40px;
    width: 80px;
    border: none;
    font-size: 20px;
    background-color: #FF6A3D;
    color: white;
    cursor: pointer;
    transition: all .1s ease-in-out;
}

.container button:hover {
    opacity: 0.86;
}

::placeholder {
    color:rgb(207, 201, 201);
}

.container input[type="text"]:focus{
    outline: none;
    box-shadow: inset 1px 1px 3px rgb(207, 201, 201);
}

.list {
    position: absolute;
    width: 100%;
    min-height: 200px;
    display: flex;
    flex-direction: column;
    left: -20px;
}

.list li {
    background-color: #8e9be6;
    text-align: center;
    color: white;
    font-size: 14px;
    line-height: 40px;
    margin-top: 1px;
    list-style: none;
    position: relative;
}

.list li i {
    position: absolute;
    top: 0;
    bottom: 0;
    right: 0;
    width: 40px;
    text-align: center;
    line-height: 38px;
    background-color: white;
    transition: all .1s linear;
    cursor: pointer;
}

.list span {
  margin-left: 20px;
}

.list span.completed {
  text-decoration: line-through;
  color: white;
}

@media screen and (max-width: 720px) {
    #app{
        width: 90%;
        max-width: 90%;
    }
}
</style>

