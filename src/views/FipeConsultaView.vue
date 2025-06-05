<template>
  <div class="container mt-4">
    <div class="row">
      <div class="col-12">
        <SearchForm @modeloSelected="handleModeloSelected" @loading="handleSearchFormLoading" @error="handleError" />
      </div>
    </div>
    <div class="row">
      <div class="col-12">
        <ResultsDisplay :veiculos="veiculos" :modeloNome="modeloNome" :loading="loadingResults" :error="error" />
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import SearchForm from '../components/fipe/SearchForm.vue';
import ResultsDisplay from '../components/fipe/ResultsDisplay.vue';
import { getVeiculos } from '../services/apiService';

const veiculos = ref([]);
const modeloNome = ref('');
const loadingResults = ref(false); // For results display specifically
const loadingSearchForm = ref(false); // For search form dependencies
const error = ref('');

async function handleModeloSelected(payload) {
  if (!payload) {
    veiculos.value = [];
    modeloNome.value = '';
    error.value = '';
    loadingResults.value = false;
    return;
  }

  const { tabela, modelo, modeloNome: mNome } = payload;
  
  loadingResults.value = true;
  error.value = '';
  veiculos.value = [];
  modeloNome.value = mNome;

  try {
    const result = await getVeiculos(tabela, modelo);
    veiculos.value = result;
  } catch (err) {
    console.error(err);
    error.value = err.message || 'Erro ao buscar veículos.';
    veiculos.value = [];
  } finally {
    loadingResults.value = false;
  }
}

// Handles loading state from SearchForm (for its internal dependencies like marcas, modelos)
function handleSearchFormLoading(isLoading) {
  loadingSearchForm.value = isLoading;
  // If search form starts loading its own data, it's a good time to clear old results/errors
  // and potentially show a loading state in ResultsDisplay as well,
  // or at least prevent new searches until form is ready.
  if (isLoading) {
    veiculos.value = [];
    // modeloNome.value = ''; // Keep modeloNome to avoid flicker if it's just a sub-selection loading
    // error.value = ''; // Don't clear error from a previous search attempt if form is just reloading
    loadingResults.value = true; // Indicate that the overall view is waiting for the form
  } else {
    // When form is done loading its dependencies, if no model is selected yet,
    // set loadingResults to false. If a model IS selected, handleModeloSelected will control it.
    if (!selectedModelo.value) { // Assuming selectedModelo is available or can be inferred
         loadingResults.value = false;
    }
  }
}

// Handles errors emitted from SearchForm (e.g., failing to load marcas)
function handleError(errorMessage) {
  error.value = errorMessage;
  veiculos.value = [];
  // modeloNome.value = ''; // Consider if model name should be cleared
  loadingResults.value = false;
  loadingSearchForm.value = false; // Ensure search form loading is also reset
}

// Need to get the selectedModelo to implement the logic in handleSearchFormLoading
// This is a placeholder, as selectedModelo is not directly available in this component.
// This indicates a potential need to refine how loading states are managed between components.
// For now, we'll assume a simplified logic.
const selectedModelo = ref(''); // Placeholder for actual selected model state

</script>

<style scoped>
/* Using Bootstrap container and row/col, so specific styles might not be needed here. */
/* Add any additional view-specific styling if necessary */
</style>
