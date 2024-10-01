<!-- composition api -->
<script setup>

import { onMounted, ref } from 'vue';
// creamos un estado para los datos, se usa ref
const name = ref('justin bilieber')
const status = ref('active')
const tasks = ref(['task one', 'task two', 'task three'])
const newTask = ref('')

// funcion que cambia el estado del usuario
const toggleStatus = () => {
  if(status.value === 'active') {
    status.value = 'pending'
  }else if (status.value === 'pending') {
    status.value = 'inactive'
  }else{
    status.value = 'active'
  }
}
// funcion para agregar tareas, cambia el estado
const addTask = () => {
  if (newTask.value.trim() !== '') {
    tasks.value.push(newTask.value)
    newTask.value = ''
  }
}

// funcion para eliminar tarea
const deleteTask = (index) => {
  tasks.value.splice(index, 1)
}

onMounted(async () => {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/todos')
    const data = await response.json()
    tasks.value = data.map((t) => t.title)
  } catch (error) {
    console.log(error)
  }
})

</script>

<template>
  <h1>Vue curso - {{ name }}</h1>
  <p v-if="status === 'active'">Usuario esta activo</p>
  <p v-else-if="status === 'pending'">Usuario esta pendiente</p>
  <p v-else>Usuario esta inactivo</p>

<!-- previene el efecto de envio -->
  <form @submit.prevent="addTask">
    <label for="newTask">Add Task</label>
    <input type="text" id="newTask" name="newTask" v-model="newTask" />
    <button type="submit">Enviar</button>
  </form>




  <h3>Tasks:</h3>
  <ul>
    <li v-for="(t, index) in tasks" :key="t">
      <span>
        {{ t }}
      </span>
      <button @click="deleteTask(index)">x</button>
    </li> 
  </ul>

  
   <br>
   <!-- <button v-on:click="toggleStatus">Change Status</button> -->
   <button @click="toggleStatus">Change Status</button>
</template>


<style scoped>
h1{
  color: chocolate;
}
</style>
