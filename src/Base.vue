<template>
<!-- Count part-->
    <p :id="`p-${count}`" :class="{active: count < 0}">
        Compteur : {{ count }} <span v-html="firstname"></span>
    </p>
    <div v-if="count >= 5">Le chiffre est supérieur ou égal à 5 Top !</div>
    <button @click="increment">Incrémenter</button>
    <button @click="decrement">Décrémenter</button>

    <hr>
<!-- Film part -->
    <div>
        <button @click="sortMovies">Réorganiser films</button>
        <form action="" @submit.prevent="addMovie">
            <input type="text" placeholder="Nouveau film" v-model="movieName"> => {{ movieName }}
            <button>Ajouter</button>
        </form>
    </div>
    <ul>
        <li
                v-for="movie in movies"
                :key="movie"
        >
            {{ movie }}
            <button @click="deleteMovie(movie)">Supprimer</button>
        </li>
    </ul>
<!-- Object part-->
<hr>
    <ul>
        <li>{{ person.firstname }}</li>
        <li>{{ person.lastname }}</li>
        <li>{{ person.age }}</li>
    </ul>
    <button @click.prevent="randomAge">Changer d'age</button>
</template>

<script setup>
import {ref} from 'vue'

const count = ref(0)
const firstname = '<span>Demo</span>'
const movieName = ref('')

const increment = (event) => {
    count.value++
}
const decrement = () => {
    count.value--
}

const movies = ref([
    'Matrix',
    'Lilo & Stitch',
    'Titanic'
])

const deleteMovie = (movie) => {
    movies.value = movies.value.filter(m => m !== movie)
}

const sortMovies = () => {
    movies.value.sort((a, b) => a > b ? 1 : -1)
}

const addMovie = () => {
    movies.value.push(movieName.value)
    movieName.value = ''
}

const person = ref({
    firstname: 'John',
    lastname: 'Doe',
    age: 20
})

const randomAge = () => {
    person.value.age = Math.round(Math.random() * 100)
}

</script>

<style>

#p-3 {
    color: green;
}

.active {
    color: red;
}

</style>