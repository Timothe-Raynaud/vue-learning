<template>
    <form action="" @submit.prevent="create = true">
        <button>Create Task</button>
    </form>

    <form action=""
          style="margin-top: 2rem"
          @submit.prevent="addTask"
          v-if="create"
    >
        <fieldset role="group">
            <input type="text" v-model="inputTitle" placeholder="Title">
            <button :disabled="inputTitle.length === 0">Ajouter</button>
        </fieldset>
    </form>

    <hr>

    <div v-if="todos.length === 0">
        Aucune tache n'est disponible
    </div>

    <div v-else>
        <ul>
            <li
                    v-for="task in sortedTodos()"
                    :key="task.date"
                    :class="{completed: task.completed}"
            >
                <label>
                    {{ task.title }}
                    <input type="checkbox" v-model="task.completed">
                </label>
            </li>
        </ul>

        <div>
            <label>
                <input type="checkbox" v-model="hideCompleted">
                Masquer les tâches complétés
            </label>
        </div>
    </div>

</template>

<script setup>
import {ref} from 'vue'

const create = ref(false)
const hideCompleted = ref(false)

const todos = ref([
    {
        title: 'Tache 1',
        completed: true,
        date: 1
    },
    {
        title: 'Tache 2',
        completed: false,
        date: 2
    },
])

const inputTitle = ref('')

const addTask = () => {
    todos.value.push({
        title: inputTitle.value,
        completed: false,
        date: Date.now()
    })

    inputTitle.value = ''
    create.value = false
}

const sortedTodos = () => {
    const sorted = todos.value.sort((a, b) => a.completed > b.completed ? 1 : -1)
    if (hideCompleted.value === true){
        return sorted.filter(t => t.completed === false)
    }
    return sorted
}

</script>

<style>
.completed{
    opacity: .5;
    text-decoration: line-through;
}
</style>
