<template>
  <div>
    <h1>
      <span v-if="!editarNombreList">{{ nombreLista }}</span>
      <span v-else>
        <input v-model="nuevoNombreLista" type="text" placeholder="Nuevo nombre de Lista">
        <button @click="guardarNuevoNombreLista">Guardar</button>
        <button @click="cancelarEdicionNombreLista">Cancelar</button>
      </span>
      <button @click="editarNombreLista">{{ editarNombreList ? 'Cancelar' : 'Editar' }}</button>
    </h1>

    <div>
      <input v-model="nuevaTarea" type="text" placeholder="Agregar nueva Tarea">
      <button @click="agregarQuehacer">Agregar</button>
    </div>

    <ul>
      <li v-for="(tarea, index) in tareas" :key="index">
        {{ tarea }}
        <button @click="eliminarTarea(index)">Eliminar</button>
        <button @click="editarTarea(index)">Editar</button>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const nombreLista = ref('Lista de Tareas');
const editarNombreList = ref(false);
const nuevoNombreLista = ref('');
const nuevaTarea = ref('');
const tareas = ref([]);

const agregarQuehacer = () => {
  if (nuevaTarea.value.trim() !== '') {
    tareas.value.push(nuevaTarea.value.trim());
    nuevaTarea.value = '';
  }
};

const eliminarTarea = (index) => {
  tareas.value.splice(index, 1);
};

const editarTarea = (index) => {
  const nuevoTexto = prompt('Editar Tarea:', tareas.value[index]);
  if (nuevoTexto !== null) {
    tareas.value[index] = nuevoTexto.trim();
  }
};

const editarNombreLista = () => {
  editarNombreList.value = true;
  nuevoNombreLista.value = nombreLista.value;
};

const cancelarEdicionNombreLista = () => {
  editarNombreList.value = false;
};

const guardarNuevoNombreLista = () => {
  nombreLista.value = nuevoNombreLista.value.trim();
  editarNombreList.value = false;
};
</script>

<style scoped>
</style>