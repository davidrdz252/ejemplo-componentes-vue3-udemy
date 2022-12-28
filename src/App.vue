<script setup>

import ButtonCounter from './components/ButtonCounter.vue'
import BlogPost from './components/BlogPost.vue';
import PaginatePost from './components/PaginatePost.vue'
import LoadingSpinnner from './components/LoadingSpinner.vue'
import { onMounted, ref } from "vue"

const posts = ref([])

//emit
const favorito = ref("");

const cambiarFavorito = (title) => {
  favorito.value = title;
};


const postxpagina = 10;
const inicio = ref(0)
const fin = ref(postxpagina)
const loading = ref(false)

// onMounted(async () => {
//   loading.value = true



// });

const fetchData = async () => {

  try {

    const res = await fetch("https://jsonplaceholder.typicode.com/posts")
    posts.value = await res.json()

  } catch (error) {
    console.log(error)
  } finally {
    setTimeout(() => {
      loading.value = false;
    }, 600);
  }

}

fetchData()

// fetch("https://jsonplaceholder.typicode.com/posts")
//       .then((res) => res.json())
//       .then((data) => {
//           posts.value = data;
//       })
//       .catch((e) => console.log(e))
//       .finally(() => {
//           setTimeout(() => {
//               loading.value = false;
//           }, 600);
//       });

const next = () => {
  inicio.value = inicio.value + postxpagina
  fin.value = fin.value + postxpagina
}

const prev = () => {
  inicio.value = inicio.value - postxpagina
  fin.value = fin.value - postxpagina
}

</script>


<template>
  <LoadingSpinnner v-if="loading"></LoadingSpinnner>
  <div class="container" v-else>

    <h1>Components</h1>
    <ButtonCounter></ButtonCounter>&nbsp
    <ButtonCounter></ButtonCounter>&nbsp
    <ButtonCounter></ButtonCounter>&nbsp
    <ButtonCounter></ButtonCounter>&nbsp<br>
    <PaginatePost class="pt-4" @siguientepaginanombre="next" @atraspaginanombre="prev" :inicio="inicio" :fin="fin"
      :cantidad="posts.length"></PaginatePost>

    <h2 class="pt-4">Mis Post Favoritos: {{ favorito }}</h2>

    <br>
    <BlogPost v-for="post in posts.slice(inicio, fin)" :key="post.id" :title="post.title" :id="post.id"
      :body="post.body" :colorText="post.colorText" @cambiarFavoritoNombre="cambiarFavorito"></BlogPost>

  </div>


</template>

<style>

</style>