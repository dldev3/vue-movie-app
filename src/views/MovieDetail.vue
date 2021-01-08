<template>
  <div class="movie-detail">
    <h2>{{ movie.Title }}</h2>
    <p>{{ movie.Year }}</p>
    <img :src="movie.Poster" alt="Movie Poster" class="featured-img" />
    <p class="genre">{{ movie.Genre }} <span class="rating">{{ (movie.imdbRating*10) }}%</span></p>
    <p>{{ movie.Plot }}</p>
  </div>
</template>

<script>

import { ref, onBeforeMount } from 'vue';
import { useRoute } from 'vue-router';
import env from '@/env.js';

export default {
 setup(){
    const movie = ref({});
    const route = useRoute();

    onBeforeMount( () => {
      fetch(`http://www.omdbapi.com/?apikey=${ env.apiKey }&i=${route.params.id}&plot=full`)
          .then(response => response.json())
          .then(data => {
            movie.value = data;
            console.log(data);
          });
    });

return {
  movie
}

  }
}

</script>

<style lang="scss">
  .movie-detail {
    padding: 16px;
    h2 {
      color:#FFF;
      font-size: 28px;
      font-weight: 800;
      margin-bottom: 16px;
    }

    .featured-img {
      display: block;
      max-width:auto;
      margin-bottom: 16px;
    }
    p {
      color: #FFF;
      font-size: 18px;
      line-height: 1.4;
      margin: 5px;
    }
    .rating {
      color:#EBD91E;
    }

    .genre {
      color:#8D8D8D;
      font-weight: 600;
    }
  }
</style>


