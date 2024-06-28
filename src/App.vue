<template>
  <div class="app">
    <header>
      <h1>The <strong>Movie</strong> Database</h1>
      <form class="search-box" v-on:submit.prevent="handleSearch">
        <input
          type="search"
          class="search-field"
          placeholder="search for a movie....."
          v-model="search_query"
        />
      </form>
    </header>

    <main>
      <div class="cards">
        <Card v-for="movie in movieList" :aa="movie"></Card>
        <!-- aa라는 이름으로 movie가 전달된다 -->
      </div>
    </main>
  </div>
</template>

<script setup>
import { onMounted, ref } from "vue";
import Card from "./components/Card.vue";

const movieList = ref([]);
const search_query = ref("");

const handleSearch = async () => {
  movieList.value = await fetch(
    `https://api.themoviedb.org/3/search/movie?query=${search_query.value}&include_adult=false&language=en-US&page=1&api_key=5fa6df004cdfe0446cb6faecb2d88543`
  )
    .then((response) => response.json())
    .then((data) => data.results);
  search_query.value = "";
};

const popular = async () => {
  movieList.value = await fetch(
    "https://api.themoviedb.org/3/movie/popular?language=en-US&page=1&api_key=5fa6df004cdfe0446cb6faecb2d88543"
  )
    .then((response) => response.json())
    .then((data) => data.results);
};

onMounted(() => {
  popular();
});
</script>

<style lang="scss" scoped>
$color: #313131;

* {
  margin: 0px;
  padding: 0px;
  box-sizing: border-box;
  font-family: sans-serif;
}
header {
  padding: 50px 0;

  h1 {
    color: rgb(206, 203, 203);
    text-align: center;
    font-weight: 400;
    text-transform: uppercase;
    font-size: 42px;
    margin-bottom: 30px;
    strong {
      color: $color;
    }
  }
}

.search-box {
  display: flex;
  justify-content: center;
  padding: 0 30px;
  .search-field {
    appearance: none;
    border: none;
    outline: none;
    padding: 15px;
    width: 100%;
    max-width: 600px;
    border-radius: 8px;
    font-size: 20px;
    color: #313131;
    background-color: #f4f4f4;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3);

    &::placeholder {
      color: #aaa;
    }

    &:focus {
      background-color: $color;
      color: #fff;
    }
  }
}

main {
  max-width: 1200px;
  margin: auto;
  padding: 0 16px;

  .cards {
    display: flex;
    flex-wrap: wrap;
  }
}
</style>
