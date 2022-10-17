<script setup>
import { ref } from "vue";
import BlogPost from "./components/BlogPost.vue";
import PaginatePost from "./components/PaginatePost.vue";
import LoadingSpinner from "./components/LoadingSpinner.vue";

const posts = ref([]);
const favorito = ref("");
const cambiarFavorito = (p) => (favorito.value = p);
const postXpagina = 10;
const inicio = ref(0);
const fin = ref(postXpagina);
const loading = ref(true);

const next = () => {
  inicio.value += 10;
  fin.value += 10;
};
const prev = () => {
  inicio.value -= 10;
  fin.value -= 10;
};

const fetchData = async () => {
  try {
    const res = await fetch("https://jsonplaceholder.typicode.com/posts");
    posts.value = await res.json();
  } catch (error) {
    console.log(error);
  } finally {
    setTimeout(() => {
      loading.value = false;
    }, 3000);
  }
};
fetchData();
</script>

<template>
  <LoadingSpinner v-if="loading"></LoadingSpinner>
  <div class="container" v-else>
    <h1>APP</h1>
    <h2>Mi post favorito: {{ favorito }}</h2>
    <PaginatePost
      @nextP="next"
      @prevP="prev"
      :inicioP="inicio"
      :finP="fin"
      :limiteP="posts.length"
    ></PaginatePost>
    <BlogPost
      v-for="post in posts.slice(inicio, fin)"
      :key="post.id"
      :title="post.title"
      :id="post.id"
      :body="post.body"
      @cFavo="cambiarFavorito"
      class="mt-2"
    ></BlogPost>
  </div>
</template>
