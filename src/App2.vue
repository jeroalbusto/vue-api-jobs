<!-- options api -->
<script>
export default {
  data(){
    return {
      name: 'justin bieber',
      status: 'pending',
      tasks: ['Task One', 'Task Two', 'Task Three'],
      link: 'https://google.com'
    }
  },
  methods:{
    toggleStatus() {
      if(this.status === 'active') {
        this.status = 'pending'
      }else if (this.status === 'pending') {
        this.status = 'inactive'
      }else{
        this.status = 'active'
      }
    }
  }
}
</script>

<template>
  <h1>Vue curso - {{ name }}</h1>
  <p v-if="status === 'active'">Usuario esta activo</p>
  <p v-else-if="status === 'pending'">Usuario esta pendiente</p>
  <p v-else>Usuario esta inactivo</p>

  <h3>Tasks:</h3>
  <ul>
    <li v-for="t in tasks" :key="t">{{ t }}</li>
  </ul>

  <!-- <a v-bind:href="link" target="_blank">google</a> -->
   <a :href="link" target="_blank">click for google</a>

   <br>
   <!-- <button v-on:click="toggleStatus">Change Status</button> -->
   <button @click="toggleStatus">Change Status</button>
</template>


<style scoped>
h1{
  color: chocolate;
}
</style>
