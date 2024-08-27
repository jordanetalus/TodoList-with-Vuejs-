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
      <li v-for="todo in sortedTodos()" 
      :key="todo.date" 
      :class="{completed: todo.completed}"> 
        <label >
          <input type="checkbox" v-model="todo.completed">
          {{ todo.title }}
        </label>
      </li>
    </ul>
    <label> 
      <input type="checkbox" v-model="hidecompleted">
      Masquer les tâches completées 
    </label>
  </div>
</template>


<script setup>
  import {ref} from 'vue'

  const hidecompleted=ref(false)
  const newTodo=ref('')
  const todos =ref([{
    title: 'tâcheTest',
    completed: true,
    date:1
  },
  {
    title: 'tâcheÀFaire',
    completed:false,
    date: 2
  }])
  const addTodo = () => {
    todos.value.push({
      title:newTodo.value,
      completed: false,
      date: Date.now()
    })
  }

  const sortedTodos = () =>{
   const sortedTodos= todos.value.toSorted((a,b)=> a.completed>b.completed? 1:-1)
   if (hidecompleted.value===true)
   {
    return sortedTodos.filter(t => t.completed ===false)
   }
   return sortedTodos
  }
  newTodo.value=''
</script>


<style>

.completed{
  opacity: .5;
  text-decoration: line-through;
}

</style>
