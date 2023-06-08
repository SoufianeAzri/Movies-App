<template>
  <div class="movie-details">
    <h2>{{movie.Title}}</h2>
    <p>{{movie.Year}}</p>
    <img :src="movie.Poster" alt="movie Poster" class="img-featured">
    <p>{{movie.Plot}}</p>
  </div>
</template>

<script>
import { ref, onBeforeMount } from "vue";
import { useRoute } from "vue-router";
import env from "@/env.js";
export default {
  setup() {
    const movie = ref({});
    const route = useRoute();
    onBeforeMount(() => {
      fetch(
        `http://www.omdbapi.com/?apikey=${env.api_key}&i=${route.params.id}&plot=full`
      )
        .then((response) => response.json())
        .then((data) => {
          movie.value = data;
        });
    });
    return {
      movie,
    };
  },
};
</script>

<style lang="scss">
.movie-details{
    padding: 16px;
    h2{
        color: #fff;
        font-size: 28px;
        font-weight: 600;
        margin-bottom: 16px;
        text-align: center;
    }
    .img-featured{
        display: block;
        max-width: 200px;
        margin: 20px auto;
        text-align: center;
    }
    p{
        color: #fff;
        line-height: 1.6;
        font-size: 14px;
        text-align: center;
    }
}
</style>