<template>
    <div class="task-list-container">
      <h1 class="text-center">Lista de Tareas</h1>
      <button @click="fetchTasks" class="btn btn-primary mb-3">
        <i class="bi bi-arrow-clockwise"></i> Cargar Tareas
      </button>
  
      <div v-if="tasks.length > 0" class="task-list">
        <div v-for="task in tasks" :key="task.id" class="task-item d-flex justify-content-between align-items-center">
          <div>
            <h5 :style="{ textDecoration: task.completed ? 'line-through' : 'none', color: task.completed ? 'green' : '#333' }" class="task-text">
              {{ task.todo }}
            </h5>
            <span class="task-status" :class="{ completed: task.completed }">
              {{ task.completed ? 'Completada' : 'Pendiente' }}
            </span>
          </div>
          <div>
            <button @click="toggleTaskCompletion(task)" class="btn btn-sm">
              <i :class="task.completed ? 'bi bi-check-circle' : 'bi bi-circle'"></i>
            </button>
            <button @click="deleteTask(task)" class="btn btn-sm">
              <i class="bi bi-trash"></i>
            </button>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    name: "TaskList",
    data() {
      return {
        tasks: []
      };
    },
    methods: {
      async fetchTasks() {
        try {
          const response = await axios.get("https://dummyjson.com/todos");
          this.tasks = response.data.todos;
        } catch (error) {
          console.error("Error al cargar tareas:", error);
        }
      },
  
      async deleteTask(task) {
        try {
          await axios.delete(`https://dummyjson.com/todos/${task.id}`);
          this.tasks = this.tasks.filter((t) => t.id !== task.id);
        } catch (error) {
          console.error("Error al eliminar tarea:", error);
        }
      },
  
      toggleTaskCompletion(task) {
        task.completed = !task.completed;
      }
    }
  };
  </script>
  
  <style scoped>
  .task-list-container {
    padding: 20px;
    max-width: 500px;
    margin: 0 auto;
  }
  
  h1 {
    text-align: center;
    color: #333;
  }
  
  .task-list {
    margin-top: 20px;
  }
  
  .task-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    background-color: #f9f9f9;
    padding: 15px;
    border-radius: 5px;
    margin-bottom: 10px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  }
  
  .task-text {
    font-size: 18px;
    color: #333;
  }
  
  .task-status {
    font-size: 14px;
    color: #888;
  }
  
  .task-status.completed {
    color: green;
    text-decoration: none;
  }
  
  .task-item .btn {
    background-color: transparent;
    border: none;
    cursor: pointer;
    color: #007bff;
  }
  
  .task-item .btn:hover {
    opacity: 0.8;
  }
  
  .task-item .btn i {
    margin-right: 5px;
  }
  
  .btn-primary {
    background-color: #007bff;
    border: none;
    color: white;
  }
  
  .btn-primary:hover {
    background-color: #0056b3;
  }
  </style>
  