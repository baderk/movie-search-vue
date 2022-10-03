<script setup>
import { ref, onBeforeMount } from "vue";
import { useRoute } from "vue-router";
import env from "../env";

const movie = ref({});
const route = useRoute();

onBeforeMount(() => {
  fetch(`${env.API_URL}&apikey=${env.API_KEY}&i=${route.params.id}&plot=full`)
    .then((res) => res.json())
    .then((data) => {
      movie.value = data;
    });
});
</script>

<template>
  <div id="movie-view">
    <img :src="movie.Poster" />
    <div class="m-10">
      <h1>{{ movie.Title }}</h1>
      <span class="text-slate-500"> {{ movie.Year }} </span>
      <p class="max-w-md">{{ movie.Plot }}</p>
    </div>
  </div>
</template>

<style lang="scss">
#movie-view {
  @apply flex flex-row m-10;

  img {
    @apply max-w-md;
  }
  p {
    @apply mt-4;
  }
}
</style>
