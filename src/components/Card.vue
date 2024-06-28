<template>
  <div class="card">
    <a :href="'https://www.themoviedb.org/movie/' + aa.id">
      <figure>
        <img
          v-if="aa.poster_path"
          :src="
            'https://image.tmdb.org/t/p/w600_and_h900_bestv2' + aa.poster_path
          "
          :alt="aa.title"
        />
        <img
          v-else
          src="http://placehold.it/200x300/ddd/333?text=MoviePoster"
          :alt="aa.title"
        />
      </figure>
      <div class="text">
        <h3>{{ aa.title }}</h3>
      </div>
    </a>
  </div>
</template>

<script setup>
const props = defineProps(["aa"]);
</script>

<style lang="scss">
$tablet: "(max-width: 860px)";
$mobile: "(max-width: 600px)";

.card {
  padding: 16px;
  width: 25%;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3);

  @media #{$tablet} {
    width: 33.33%;
  }

  @media #{$mobile} {
    width: 50%;
  }

  a {
    text-decoration: none;
    display: block;
    border-radius: 8px;
    overflow: hidden;
    margin: 10px;

    figure {
      width: 100%;
      height: 360px;
      overflow: hidden;
      margin: 0;

      img {
        width: 100%;
        height: 100%;
        object-fit: cover;
        transition: 0.3s;
      }
    }

    .text {
      height: 80px;
      padding: 16px;

      h3 {
        color: #313131;
        font-size: 16px;
      }
    }
  }
  &:hover img {
    transform: scale(1.1);
  }
  &:hover a h3 {
    color: forestgreen;
  }
}
</style>
