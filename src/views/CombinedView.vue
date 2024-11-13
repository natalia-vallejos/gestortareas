<template>
    <div class="combined-view-container">
      <h1>Lista de Tareas Combinada</h1>

      <div class="input-group">
        <input 
          v-model="newTask" 
          @keyup.enter="addTask" 
          placeholder="Añadir nueva tarea" 
          class="task-input"
        />
        <button @click="addTask" class="add-button">
          <i class="bi bi-plus-circle"></i> Añadir
        </button>
      </div>
  
      <!-- Tareas cargadas desde la API -->
      <div v-if="tasks.length > 0" class="task-list">
        <div v-for="task in tasks" :key="task.id" class="task-item">
          <div class="task-info">
            <span :class="{ completed: task.completed }">{{ task.todo }}</span>
            <div class="task-status" :class="{ completed: task.completed }">
              {{ task.completed ? 'Completada' : 'Pendiente' }}
            </div>
          </div>
          <div>
            <!-- Botón para marcar tarea como completada o no completada -->
            <button @click="toggleTaskCompletion(task)" class="btn btn-sm">
              <i :class="task.completed ? 'bi bi-check-circle' : 'bi bi-circle'"></i>
            </button>
            <!-- Botón para eliminar tarea -->
            <button @click="deleteTask(task)" class="btn btn-sm">
              <i class="bi bi-trash"></i>
            </button>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: "CombinedView",
    data() {
      return {
        newTask: "", // Para la tarea nueva
        tasks: [],   // Lista de tareas
      };
    },
    methods: {
      addTask() {
        if (this.newTask.trim() === "") return;
  
        // Crear una nueva tarea y agregarla
        const newTask = {
          todo: this.newTask,
          completed: false,
          id: Date.now(),
        };
  
        this.tasks.unshift(newTask);
        this.newTask = ""; // Limpiar el campo de texto
      },
  
      toggleTaskCompletion(task) {
        // Cambiar el estado de completado
        task.completed = !task.completed;
      },
  
      deleteTask(task) {
        // Eliminar la tarea
        this.tasks = this.tasks.filter((t) => t.id !== task.id);
      },
  
      // Aquí podrías agregar el código para cargar las tareas desde la API si lo necesitas
      fetchTasks() {
        // Ejemplo de API: 'https://dummyjson.com/todos'
        fetch('https://dummyjson.com/todos')
          .then((response) => response.json())
          .then((data) => {
            this.tasks = data.todos; 
          });
      }
    },
    mounted() {
      // Cargar tareas al montar el componente
      this.fetchTasks();
    },
  };
  </script>
  
  <style scoped>
  .combined-view-container {
    padding: 20px;
    max-width: 500px;
    margin: 0 auto;
  }
  
  .input-group {
    display: flex;
    margin-bottom: 10px;
  }
  
  .task-input {
    flex-grow: 1;
    padding: 8px;
    margin-right: 5px;
    border: 1px solid #ccc;
    border-radius: 4px;
  }
  
  .add-button {
    padding: 8px 12px;
    border: none;
    border-radius: 4px;
    background-color: #007bff;
    color: white;
    cursor: pointer;
  }
  
  .add-button i {
    margin-right: 5px;
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
  
  .task-info {
    display: flex;
    flex-direction: column;
  }
  
  .task-text {
    font-size: 18px;
    color: #333;
  }
  
  .task-status {
    font-size: 14px;
    color: #888;
    margin-top: 5px;
  }
  
  .task-status.completed {
    color: green;
    text-decoration: none
  }
  
  .completed {
    text-decoration: line-through;
    color: green;
  }
  
  .btn {
    background: none;
    border: none;
    cursor: pointer;
    color: #007bff;
  }
  
  .btn i {
    font-size: 1.2rem;
  }
  
  .btn:hover {
    color: #0056b3;
  }
  </style>
  