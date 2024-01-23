<template>
  <div id="app" class="container">
    <h1 class="title">Melero y Eloy los mejores</h1>
    <h2>Cambios realizados para la V2</h2>
    <h3>Lista de usuarios</h3>
    <div v-if="apiData" class="user-list">
      <ul>
        <li v-for="user in apiData" :key="user.id" class="user-item">{{ user.name }}</li>
      </ul>
    </div>
    <div v-else class="loading">
      <p>Cargando datos...</p>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const apiData = ref(null)

onMounted(async () => {
  try {
    const response = await fetch('https://apimocha.com/profesor/users')
    if (!response.ok) {
      throw new Error('Error en la solicitud de la API')
    }
    apiData.value = await response.json()
  } catch (error) {
    console.error('Error fetching API data:', error.message)
  }
})
</script>

<style scoped>
.container {
  max-width: 600px;
  margin: 0 auto;
  text-align: center;
  padding: 20px;
}

.title {
  font-size: 24px;
  margin-bottom: 20px;
  color: #333;
}

.user-list {
  border: 1px solid #ccc;
  padding: 10px;
  border-radius: 5px;
  background-color: #f8f8f8;
}

.user-item {
  list-style-type: none;
  margin: 5px 0;
  padding: 10px;
  background-color: #fff;
  border: 1px solid #ddd;
  border-radius: 5px;
}

.loading {
  margin-top: 20px;
  font-style: italic;
  color: #888;
}
</style>
