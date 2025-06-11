<template>
  <div class="container">
    <p v-show="totalTask < 1">Jusqu'ici, vous n'avez aucune tâche à faire</p>

    <form @submit.prevent="submitTask(actualTask)" action="">
      <input
        type="text"
        placeholder="Ecrivez une tâche ici.."
        v-model="actualTask"
      />
      <button>Ajouter une tâche</button>
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
  justify-content: center;
  align-items: center;
  box-shadow: rgba(0, 0, 0, 0.12) 0px 1px 3px,
              rgba(0, 0, 0, 0.24) 0px 1px 2px;
  background-color: rgb(46, 62, 114);
  padding: 40px;
  border-radius: 10px;
}

#app {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  color: rgb(0, 0, 0);
  background-color: rgb(33, 43, 78);
}

p {
  color: white;
}

li {
  color: rgb(255, 255, 255);
  list-style: none;
}

ul {
  border-radius: 1% / 62%;
  margin: 3px;
  background-color: rgb(12, 28, 44);
  list-style-type: none;
  padding-right: 17%;
}

form {
  background-color: rgb(244, 244, 244);
  padding: 30px;
  border-radius: 5px;
  box-shadow: rgba(6, 24, 44, 0.4) 0px 0px 0px 2px,
    rgba(6, 24, 44, 0.65) 0px 4px 6px -1px,
    rgba(255, 255, 255, 0.08) 0px 1px 0px inset;
  display: flex;
  gap: 41px;
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

button:hover {
  background-color: orange;
}
</style>
