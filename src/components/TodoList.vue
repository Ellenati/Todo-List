
<template>
  <div>
    <h1>Todo List</h1>

    <!-- Formulario para adicionar tarefas -->
    <div class="input-container">
      <input v-model="newTask" placeholder="Nova tarefa" />
      <button class="add-task-btn" @click="addTask">✚</button>
    </div>

    <!-- Lista de Tarefas -->
    <div class="task-list">
      <div v-for="(task, index) in tasks" :key="index" class="task-item" :class="{ completed: task.completed }">
        <span class="task-title">{{ task.title }}</span>

        <!-- Botões para marcar como lido e deletar -->
        <div class="task-actions">
          <button class="complete-btn" @click="toggleCompleted(index)">✔</button>
          <button class="delete-btn" @click="deleteTask(index)">✖</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

// Lista de tarefas e nova tarefa
const tasks = ref([]);
const newTask = ref('');

// Função para adicionar uma nova tarefa
function addTask() {
  if (newTask.value.trim()) {
    tasks.value.push({ title: newTask.value, completed: false });
    newTask.value = '';
  }
}

// Função para deletar uma tarefa
function deleteTask(index) {
  tasks.value.splice(index, 1);
}

// Função para marcar e desmarcar tarefa como lida
function toggleCompleted(index) {
  tasks.value[index].completed = !tasks.value[index].completed;
}
</script>


<!-- Por algum motivo não estou conseguindo referenciar o css em um 
arquivo separado então tive que deixar tudo junto no mesmo arquivo -->
<style>

body {
  font-family: Arial, sans-serif;
  background-color: #f9f9f9;
  padding: 20px;
}

h1 {
  text-align: center;
  color: #333;
}

.input-container {
  display: flex;
  justify-content: center;
  margin-bottom: 20px;
}

input {
  width: 300px;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  margin-right: 10px;
}

.add-task-btn {
  padding: 10px 20px;
  background-color: #4CAF50;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.add-task-btn:hover {
  background-color: #45a049;
}

.task-list {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.task-item {
  background-color: #f4f4f4;
  border: 1px solid #ddd;
  border-radius: 8px;
  padding: 15px;
  margin-bottom: 10px;
  width: 400px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
}

.completed {
  background-color: #d1ffd1;
  text-decoration: line-through;
}

.task-title {
  font-size: 18px;
}

.task-actions {
  display: flex;
  gap: 10px;
}

.complete-btn {
  background-color: #4CAF50;
  color: white;
  border: none;
  padding: 10px;
  border-radius: 5px;
  cursor: pointer;
  font-size: 18px;
}

.complete-btn:hover {
  background-color: #45a049;
}

.delete-btn {
  background-color: #f44336;
  color: white;
  border: none;
  padding: 10px;
  border-radius: 5px;
  cursor: pointer;
  font-size: 18px;
}

.delete-btn:hover {
  background-color: #e53935;
}
</style>
