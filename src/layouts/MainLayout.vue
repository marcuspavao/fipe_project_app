<template>
  <div>
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
      <div class="container">
        <a class="navbar-brand fs-4" href="#"><i class="fas fa-car" /> Consulta Tabela FIPE</a>
        <button
          class="navbar-toggler"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#navbarNav"
          aria-controls="navbarNav"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
          <ul class="navbar-nav ms-auto">
            <li class="nav-item">
              <router-link class="nav-link" to="/">Consulta FIPE</router-link>
            </li>
            <li class="nav-item">
              <router-link class="nav-link" to="/comparar">Comparar Valores</router-link>
            </li>
            <li class="nav-item">
              <router-link class="nav-link" to="/dashboard">Dashboard Marcas</router-link>
            </li>
          </ul>
        </div>
      </div>
    </nav>

    <main class="container mt-4">
      <router-view />
    </main>

    <footer class="bg-dark text-white text-center py-3 mt-4">
      <div class="container">
        <p class="mb-0">Dados fornecidos pela Tabela FIPE &copy; 2025</p>
      </div>
    </footer>
  </div>
</template>

<script setup>
// No script needed for now
</script>

<style scoped>
</style>