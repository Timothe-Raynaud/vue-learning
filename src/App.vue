<template>

    <form action="" @submit.prevent="create = true">
        <button>Create Task</button>
    </form>

    <form action=""
          @submit.prevent="addTask"
          v-if="create"
    >
        <input type="text" v-model="inputTitle" placeholder="title">
        <input type="text" v-model="inputDescription" placeholder="description">
        <button>Submit</button>
    </form>

    <hr>

    <div v-if="todolist.length === 0">
        Aucune tache n'est disponible
    </div>

    <div v-else>
        <ul>
            <li v-for="task in todolist">
                <div>{{ task.title }}</div>
                <div>{{ task.description }}</div>
                <input type="checkbox" @toggle="sortTask" value="{{ task.statut }}">
            </li>
        </ul>
    </div>

</template>

<script setup>
import {ref} from 'vue'

const create = ref(false)
const todolist = ref([])

const inputTitle = ref('')
const inputDescription = ref('')

const addTask = () => {
    console.log(inputTitle.value, inputDescription.value)
    todolist.value.push({
        title: inputTitle.value,
        description: inputDescription.value,
        statut: false
    })

    inputTitle.value = inputDescription.value = ''
    create.value = false
}

const sortTask = () => {
    console.log('test')
    todolist.value.sort((a,b) => console.log(a, b))
}

</script>

<style>
.active {
    font-size: 1.3rem;
}
</style>
