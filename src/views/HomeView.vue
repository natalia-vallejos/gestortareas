<template>
  <div class="home">
    <div class="container">
      <!-- Título y descripción -->
      <h1 class="text-center text-primary">Bienvenido a la Aplicación de Tareas con Vue</h1>
      <p class="lead text-center">Esta aplicación te permite gestionar tus tareas de manera eficiente. Puedes añadir nuevas tareas manualmente o extraerlas desde una API.</p>
      
      <!-- Logo Vue -->
      <div class="logo-container text-center">
        <img alt="Vue logo" src="../assets/logo.png" class="logo">
      </div>
      
      <!-- Secciones de la aplicación -->
      <div class="sections text-center mt-5">
        <h3>Secciones de la Aplicación</h3>
        <ul class="list-unstyled">
          <li><strong>Añadir Tarea:</strong> Permite ingresar nuevas tareas manualmente.</li>
          <li><strong>Lista de Tareas:</strong> Muestra todas las tareas extraídas desde la API, permitiendo marcarlas como completadas o eliminarlas.</li>
          <li><strong>Vista Combinada:</strong> Combina las funcionalidades de añadir tareas manualmente y las tareas de la API al mismo tiempo.</li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HomeView'
}
</script>

<style scoped>
.home {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  padding: 50px 0;
}

h1 {
  font-size: 36px;
  font-weight: bold;
}

.lead {
  font-size: 18px;
}

.logo-container {
  margin-top: 30px;
}

.logo {
  width: 150px; 
  border-radius: 50%;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
}

.sections {
  margin-top: 50px;
}

.sections h3 {
  font-size: 28px;
  color: #42b983;
}

.sections ul {
  list-style-type: none;
  padding: 0;
}

.sections li {
  font-size: 18px;
  line-height: 1.5;
}

.sections li strong {
  font-weight: bold;
}
</style>
