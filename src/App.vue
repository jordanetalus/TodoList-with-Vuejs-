<template>
  <form action="" @submit.prevent="addTodo">

    <fieldset role="group">
      <input type="text" placeholder="tache à effectuer " v-model="newTodo"  >
      <button :disabled="newTodo.length === 0">Ajouter</button>
    </fieldset>
  </form>

  <div v-if="todos.length === 0">
    <p>Vous n'avez pas de tâche à faire :( </p>
  </div>
  <div v-else>
    <ul>
      <li v-for="todo in todos" :key="todo.date"> {{ todo.title }} </li>
    </ul>
  </div>
</template>


<script setup>
  import {ref} from 'vue'

  const newTodo=ref('')
  const todos =ref([])
  const addTodo = () => {
    todos.value.push({
      title:newTodo.value,
      completed: false,
      date: Date.now()
    })
  }
</script>


<style scoped>

</style>
