<script setup>
import { defineProps, onMounted } from 'vue';
import { useMovieStore } from '@/stores/movie';
const movieStore = useMovieStore();

const props = defineProps({
  movieId: {
    type: Number,
    required: true,
  },
});

onMounted(async () => {
  await movieStore.getMovieDetail(props.movieId);
});
</script>

<template>
  <div class="d1">
    <div class="body">
      <div class="main">
        <div class="content">
          <img :src="`https://image.tmdb.org/t/p/w185${movieStore.currentMovie.poster_path}`"
            :alt="movieStore.currentMovie.title" />

          <div class="details">
            <h1>Filme: {{ movieStore.currentMovie.title }}</h1>
            <p>{{ movieStore.currentMovie.tagline }}</p>
            <p>{{ movieStore.currentMovie.overview }}</p>
            <p>Orçamento: ${{ movieStore.currentMovie.budget }}</p>
            <p>Avaliação: {{ movieStore.currentMovie.vote_average }}</p>
          </div>
        </div>
      </div>

      <p class="product">Produtoras</p>
      <div class="companies">
        <template v-for="company in movieStore.currentMovie.production_companies" :key="company.id">
          <img v-if="company.logo_path" :src="`https://image.tmdb.org/t/p/w92${company.logo_path}`"
            :alt="company.name" />
          <p v-else>{{ company.name }}</p>
        </template>
      </div>
    </div>
  </div>
</template>

<style scoped>
.product {
  margin: 2rem 0;
  font-size: 1.5rem;
  font-weight: bold;
  color: white;
}
h1{
    margin-bottom: 30px;
}
.details p:not(:first-of-type) {
  margin-top: 0.6rem;
    
}
.d1 {
  display: flex;
  justify-content: center;
  margin-top: 2vw;
}

.content {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 2rem;
  margin-bottom: 2rem;
}

.content p {
  width: 80%;
}
.content img{
  margin-right: 1vw;
}
.body {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 2rem;
  background-color: #2a2a2a;
  width: 50%;
  border-radius: 20px;
  color: white;
}

.companies {
  display: flex;
  justify-content: center;
  flex-direction: row;
  column-gap: 3rem;
  align-items: center;
  margin-bottom: 2rem;
}
</style>