<script setup>
import axios from "axios";
import { ref, onMounted } from 'vue';
import { useRouter } from "vue-router";

const props = defineProps(["genres"]);
const router = useRouter();
const selectedGenre = ref(28);
const response = ref(null);

async function getMovieByGenre() {
  response.value = await axios.get(`https://api.themoviedb.org/3/discover/movie?api_key=${import.meta.env.VITE_TMDB_KEY}&with_genres=${selectedGenre.value}`);
}

function getMovieDetails(id) {
  router.push(`/movies/${id}`)
}

onMounted(async () => {
  response.value = await axios.get(`https://api.themoviedb.org/3/discover/movie?api_key=${import.meta.env.VITE_TMDB_KEY}&with_genres=${selectedGenre.value}`);
})
</script>

<template>
  <div class="movie-gallery">
    <select v-model="selectedGenre" @change="getMovieByGenre()">
      <option v-for="genre of genres" :value="genre.id">{{ genre.genreName }}</option>
    </select>
    <div v-if="response" class="movie-list">
      <div v-for="movie in response.data.results" :key="movie.id" class="movie-card" @click="getMovieDetails(movie.id)">
        <img :src="`https://image.tmdb.org/t/p/w500${movie.poster_path}`" alt="Movie Poster" class="movie-poster" />
        <p class="movie-title">{{ movie.title }}</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.image-gallery {
    display: flex;
    justify-content: center; 
    gap: 30px; 
    margin: 20px 0; 
}

.image-gallery img {
    width: 10%; 
    height: auto; 
    object-fit: cover;
    border-radius: 10px; 
    transition: transform 0.3s, filter 0.3s; 
}

.image-gallery img:hover {
    transform: scale(1.1); 
    filter: brightness(1.15); 
}
</style>