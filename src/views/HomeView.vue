<script setup>
import { ref } from "vue";
import env from "../env";

const search = ref("");
const moviesList = ref([]);

const error = ref("");

const searchMovie = () => {
  if (search.value !== "") {
    fetch(`${env.API_URL}&apikey=${env.API_KEY}&s=${search.value}`)
      .then((res) => res.json())
      .then((data) => {
        // if movie is found
        if (data.Search) {
          error.value = "";

          moviesList.value = data.Search;
        } else {
          error.value = data.Error;
          moviesList.value = [];
        }
      })
      .catch((err) => console.log(err));
  } else {
    moviesList.value = [];
    error.value = "Type something first";
  }
  search.value = "";
};
</script>

<template>
  <main>
    <div class="flex justify-center items-center">
      <input
        type="text"
        v-model="search"
        placeholder="Search movies"
        @keydown.enter="searchMovie()"
      />
      <button @click="searchMovie()" class="btn btn-fuchsia">Search</button>
    </div>

    <div class="flex justify-center items-center text-red-500">
      {{ error }}
    </div>

    <div id="movies-list">
      <div
        id="movie-card"
        class="relative"
        v-for="movie in moviesList"
        :key="movie.imdbID"
      >
        <img :src="movie.Poster" />
        <RouterLink
          class="hover:underline font-semibold"
          :to="'/movie/' + movie.imdbID"
        >
          {{ movie.Title }}
        </RouterLink>
        <p class="text-slate-500">{{ movie.Year }}</p>
      </div>
    </div>
  </main>
</template>

<style lang="scss">
#movies-list {
  @apply flex flex-wrap ml-10;
  @apply justify-center;
}
#movie-card {
  @apply m-4 w-52;
  img {
    @apply block h-72;
  }
}

input {
  &[type="text"] {
    @apply w-64 h-9 m-5 pl-1;
    @apply bg-zinc-600 rounded-sm;
    @apply placeholder:italic placeholder:text-slate-300 focus:shadow;
  }
}
</style>
