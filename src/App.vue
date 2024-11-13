<template>
  <div id="app">
    <nav class="navbar navbar-expand-lg navbar-light bg-light shadow-sm">
      <div class="container">
        <router-link to="/" class="navbar-brand">
          <i class="bi bi-house-door-fill"></i> Home
        </router-link>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
          <ul class="navbar-nav ms-auto">
            <li class="nav-item">
              <router-link to="/addtask" class="nav-link">
                <i class="bi bi-plus-circle-fill"></i> Agregar Tarea
              </router-link>
            </li>
            <li class="nav-item">
              <router-link to="/tasklist" class="nav-link">
                <i class="bi bi-list-check"></i> Listas de tareas
              </router-link>
            </li>
            <li class="nav-item">
              <router-link to="/combinedview" class="nav-link">
                <i class="bi bi-columns-gap"></i> Vista combinada
              </router-link>
            </li>
          </ul>
        </div>
      </div>
    </nav>
    <router-view/>
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 15px;
  
}

nav .navbar-nav .nav-link {
  font-weight: bold;
  color: #2c3e50;
  padding: 8px 15px;
}

nav .navbar-nav .nav-link:hover {
  background-color: #f8f9fa;
  color: #2841af;
}

nav .navbar-nav .router-link-exact-active {
  color: #2841af;
}

.navbar-brand {
  font-weight: bold;
  color: #2c3e50;
  display: flex;
  align-items: center;
}

.navbar-toggler {
  border-color: blue;
}

.navbar-nav .nav-link i {
  margin-right: 8px;
}
</style>
