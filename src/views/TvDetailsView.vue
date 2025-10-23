<script setup>
import { defineProps, onMounted } from 'vue';
import { useTvStore } from '@/stores/tv';
const tvStore = useTvStore();

const props = defineProps({
    tvId: {
        type: Number,
        required: true,
    },
});

onMounted(async () => {
    await tvStore.getTvDetail(props.tvId);
});
</script>

<template>
    <div class="d1">
        <div class="body">
            <div class="main">
                <div class="content">
                    <img :src="`https://image.tmdb.org/t/p/w185${tvStore.currentTv.poster_path}`"
                        :alt="tvStore.currentTv.title" />

                    <div class="details">
                        <h1>Programa de TV: {{ tvStore.currentTv.name }}</h1>
                        <p>{{ tvStore.currentTv.tagline }}</p>
                        <p>{{ tvStore.currentTv.overview }}</p>
                        <p>Temporadas: {{ tvStore.currentTv.number_of_seasons }}</p>
                        <p>Avaliação: {{ tvStore.currentTv.vote_average }}</p>
                    </div>
                </div>
            </div>

            <p class="product">Produtoras</p>
            <div class="companies">
                <template v-for="company in tvStore.currentTv.production_companies" :key="company.id">
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
.d1 {
  display: flex;
  justify-content: center;
  margin-top: 2vw;
}
h1{
    margin-bottom: 30px;
}

.details p:not(:first-of-type) {
  margin-top: 0.6rem;
    
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
    border-radius: 10px;
    box-shadow: 0 0 0.5rem #000;
    margin-right: 1vw;
}

.body {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 2rem;
  background-color: #363636;
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