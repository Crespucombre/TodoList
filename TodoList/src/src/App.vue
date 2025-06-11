<template>
  <div class="container">
    <p v-show="totalTask < 1">Jusqu'ici, vous n'avez aucune tâche à faire</p>
    <form @submit.prevent="submitTask(actualTask)" action="">
      <button>Ajouter une tâche</button>
      <input
        type="text"
        placeholder="Ecrivez une tâche ici.."
        v-model="actualTask"
      />
    </form>
    <ul>
      <li
        :style="{
          textDecoration: task.isCompleted ? 'line-through' : '',
        }"
        v-for="task in tasks"
      >
        <input type="checkbox" @click="setDid(task)" name="" id="" />
        {{ task.title }}
        {{ task.isCompleted ? "Fait" : "A faire" }}
        {{ "le " + task.date }}
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref } from "vue";

const tasks = ref([]);
const actualTask = ref("");
const totalTask = ref(0);

const date = new Date();

class Task {
  title = "";
  isCompleted = false;
  date = date.toLocaleDateString();
}

const setDid = (task) => {
  task.isCompleted = !task.isCompleted;
};

const submitTask = () => {
  const taskToDeploy = new Task();
  taskToDeploy.title = actualTask.value;
  tasks.value.push(taskToDeploy);
  totalTask.value++;
  actualTask.value = "";
};
</script>

<style>
.container {
  display: flex;
  flex-direction: column;
  justify-content: center; /* centre verticalement */
  align-items: center; /* centre horizontalement */
  height: 100vh;
  background-color: rgb(27, 69, 97);
  margin: none;
}
#app {
  color: beige;
  background-color: rgb(39, 51, 61);
}

li {
  color: white;
}

ul {
  list-style-type: none;
}

form {
  display: flex;
  gap: 10px;
}

input {
  flex: 1;
  padding: 8px;
  font-size: 16px;
}

button {
  margin: 20px;
  padding: 8px 16px;
  font-size: 16px;
}
</style>
