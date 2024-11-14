<template>
  <div v-if="todolist.length === 0">Aucune tache n'est disponible</div>

  <form action="" @submit.prevent="">
      <button>Create Task</button>
  </form>

  <form action="" @submit.prevent="" v-bind:id="taskId">

  </form>

  <div v-else>
    <ul>
        <li v-for="task in todolist">
            <div>{{ task.title }}</div>
            <div>{{ task.description }}</div>
            <input type="checkbox" value="{{ task.statut }}">
        </li>
    </ul>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const todolist = ref([])

const task = ref({
    title: '',
    description: '',
    statut: false
})
</script>

<style>
.active {
    font-size: 1.3rem;
}
</style>
