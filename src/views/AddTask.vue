<template>
    <div class="add-task-container">
      <h1>Añadir Tarea</h1>
      <div class="input-group mb-3">
        <input 
          v-model="newTask" 
          @keyup.enter="addTask" 
          placeholder="Añadir nueva tarea" 
          class="task-input form-control"
        />
        <button @click="addTask" class="add-button btn">
          <i class="bi bi-plus-circle"></i> Añadir
        </button>
      </div>
  
      <div v-if="tasks.length > 0" class="task-list">
        <div v-for="task in tasks" :key="task.id" class="task-item">
          <div class="task-header d-flex justify-content-between align-items-center">
            <span :class="{ completed: task.completed }" class="task-text">{{ task.todo }}</span>
            <div>
              <button @click="toggleTaskCompletion(task)" class="btn btn-sm">
                <i :class="task.completed ? 'bi bi-check-circle' : 'bi bi-circle'"></i>
              </button>
              <button @click="deleteTask(task)" class="btn btn-sm">
                <i class="bi bi-trash"></i>
              </button>
            </div>
          </div>
          <div class="task-status" :class="{ completed: task.completed }">
            {{ task.completed ? "Completada" : "Pendiente" }}
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: "AddTask",
    data() {
      return {
        newTask: "",
        tasks: [],
      };
    },
    methods: {
      // Método para agregar una tarea
      addTask() {
        if (this.newTask.trim() === "") return;
        
        const task = {
          id: Date.now(), 
          todo: this.newTask,
          completed: false,
        };
        
        this.tasks.unshift(task); 
        this.newTask = ""; 
      },
  
      deleteTask(task) {
        this.tasks = this.tasks.filter((t) => t.id !== task.id);
      },

      toggleTaskCompletion(task) {
        task.completed = !task.completed;
      },
    },
  };
  </script>
  
  <style scoped>
  .add-task-container {
    padding: 20px;
    max-width: 500px;
    margin: 0 auto;
  }
  
  h1 {
    text-align: center;
    margin-bottom: 20px;
    color: #333;
  }
  
  .input-group {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  
  .task-input {
    flex-grow: 1;
    padding: 8px;
    margin-right: 5px;
    border: 1px solid #ccc;
    border-radius: 4px;
  }
  
  .add-button {
    background-color: #007bff;
    color: white;
    padding: 10px 20px;
    border: none;
    font-size: 16px;
    cursor: pointer;
    border-radius: 5px;
  }
  
  .add-button:hover {
    background-color: #0056b3;
  }
  
  .task-list {
    margin-top: 20px;
  }
  
  .task-item {
    display: flex;
    flex-direction: column; 
    justify-content: flex-start;
    background-color: #f9f9f9;
    padding: 15px;
    border-radius: 5px;
    margin-bottom: 10px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  }
  
  .task-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  
  .task-text {
    font-size: 16px;
  }
  
  .task-item .btn {
    background-color: transparent;
    border: none;
    cursor: pointer;
    color: #2a2ccf; 
  }
  
  .task-item .btn:hover {
    opacity: 0.8;
  }
  
  .completed {
    text-decoration: line-through;
    color: green;
  }
  
  .task-status {
    font-size: 14px;
    margin-top: 10px;
    color: #888;
  }
  
  .task-status.completed {
    color: green;
    text-decoration: none
  }
  </style>
  