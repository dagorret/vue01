<script setup lang="ts">
import { ref, computed } from 'vue'
import Button from 'primevue/button'
import InputText from 'primevue/inputtext'
import Label from 'primevue/label'
import Dialog from 'primevue/dialog'
import Avatar from 'primevue/avatar'

// Estado reactivo
const nombre = ref('')
const emailModal = ref('')
const visible = ref(false)

// Computada para la pantalla principal
const mensajeHola = computed(() => {
  return nombre.value.trim() !== '' ? `Hola: ${nombre.value}!` : 'Hola!'
})
</script>

<template>
  <main class="contenedor">
    <Label for="nombre-input">{{ mensajeHola }}</Label>
    
    <InputText 
      id="nombre-input"
      v-model="nombre" 
      placeholder="Escribe tu Nombre" 
    />

    <Button @click="visible = true">ALgo Haremos</Button>

    <!-- Ventana Emergente (Dialog) -->
    <Dialog v-model:visible="visible" modal header="Editar Perfil" :style="{ width: '25rem' }">
      <template #header>
        <div style="display: flex; align-items: center; gap: 8px;">
          <Avatar image="https://primefaces.org/cdn/primevue/images/avatar/amyelsner.png" shape="circle" />
          <span style="font-weight: bold;">{{ nombre || 'Usuario' }}</span>
        </div>
      </template>

      <span style="display: block; margin-bottom: 16px; color: #666; font-size: 0.9rem;">
        Edita la información de tu perfil.
      </span>

      <div style="display: flex; flex-direction: column; gap: 10px; margin-bottom: 16px;">
        <Label for="username">Nombre:</Label>
        <!-- Mostramos y editamos la misma variable 'nombre' -->
        <InputText id="username" v-model="nombre" placeholder="Nombre completo" />
      </div>

      <div style="display: flex; flex-direction: column; gap: 10px; margin-bottom: 16px;">
        <Label for="email">Email:</Label>
        <InputText id="email" v-model="emailModal" placeholder="correo@ejemplo.com" />
      </div>

      <template #footer>
        <Button label="Cancelar" text severity="secondary" @click="visible = false" />
        <Button label="Guardar" severity="primary" @click="visible = false" />
      </template>
    </Dialog>
  </main>
</template>

<style scoped>
.contenedor {
  display: flex;
  flex-direction: column;
  gap: 12px;
  max-width: 300px;
  margin: 40px auto;
  font-family: sans-serif;
}
</style>