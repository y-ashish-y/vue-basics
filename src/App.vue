<!-- Options API example used in version2 -->

<script lang="ts" setup>
import { ref } from "vue";

// Composition API example used in version3
// ref() is a function that creates a reactive reference to a value.
// It is used to create reactive data properties in Vue 3.
// The ref() function takes an initial value as an argument and returns a reactive reference object.
// The value of the reference can be accessed and modified using the .value property.

const name = ref("John Doe");
const status = ref("active");
const tasks = ref(["TaskOne", "TaskTwo", "TaskThree"]);
const link = ref("https://google.com");

const newTask = ref("");

const toggleStatus = () => {
  if (status.value === "active") {
    status.value = "pending";
  } else if (status.value === "pending") {
    status.value = "inactive";
  } else {
    status.value = "active";
  }
};

const addTask = () => {
  if (newTask.value.trim() !== "") {
    tasks.value.push(newTask.value);
    newTask.value = ""; // Clear the input field after adding the task
  }
};

const deleteTask = (index: number) => {
  tasks.value.splice(index, 1);
};
</script>

<template>
  <h1>{{ name }}</h1>
  <p v-if="status === 'active'">User is active</p>
  <p v-else-if="status === 'pending'">User is pending</p>
  <p v-else>User is inactive</p>
  <form @submit.prevent="addTask">
    <label for="task">Add Task</label>
    <input type="text" id="task" v-model="newTask" />
    <!-- V-model lets us binds inputs to the variables -->
    <button type="submit">Submit</button>
  </form>
  <h3>Tasks</h3>
  <ul>
    <li v-for="(task, index) in tasks" :key="task">
      <span>
        {{ task }}
      </span>
      <button @click="deleteTask(index)">x</button>
    </li>
  </ul>
  <!-- <a v-bind:href="link">Click for Google</a> -->
  <a :href="link">Click for Google</a>
  <br />
  <!-- Using : means its dynamic -->
  <!-- <button v-on:click="toggleStatus">Change Status</button> -->
  <button @click="toggleStatus">Change Status</button>
  <!-- @ Attaches an event listener to the element. -->
</template>
