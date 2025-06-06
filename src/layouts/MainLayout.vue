<template>
  <div>
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
      <div class="container">
        <a class="navbar-brand fs-4" href="#"><img src="../../images/icon_white.png" alt="Ícone de Carro" height="50"></a>        <button
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

    <main>
      <router-view />
    </main>

    <footer class="bg-dark text-white text-center py-3">
      <div class="container">
        <p class="mb-0">Dados fornecidos pela Tabela FIPE &copy; 2025</p>
      </div>
    </footer>
  </div>
</template>

<script setup>
</script>

<style scoped>
</style>