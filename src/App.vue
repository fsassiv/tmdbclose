<template>
  <div id="app">
    <div class="container">
      <input
        type="search"
        class="app__search-input"
        placeholder="Busque um filme por nome, ano ou gênero"
        v-model="keyword"
        @keyup.enter="runSearch(keyword)"
      >
      <div v-if="!movieList">
        <h3>The Movie db Clone by Flavio Andrade</h3>
        <br>
        <p>
          <a
            href="https://fsassiv.github.io/portfolio/projectName/"
            target="_blank"
          >Github Portfólio</a>
        </p>
      </div>
      <!-- LOAD RESULTS -->
      <ul class="app__movie-list">
        <app-movies
          :key="movie.id"
          v-for="movie in movieList.results"
          :movie-id="movie.id"
          :posterUrl="movie.poster_path"
          :title="movie.title"
          :description="movie.overview"
          :vote_average="movie.vote_average"
          :date="movie.release_date"
        ></app-movies>
      </ul>
      <!-- PAGINATION -->
      <!-- <ul class="app__pagination">
        <li class="app__pagination-item">
          <a href class="app__pagination-link">1</a>
        </li>
        <li class="app__pagination-item">
          <a href class="app__pagination-link">2</a>
        </li>
        <li class="app__pagination-item">
          <a href class="app__pagination-link active">3</a>
        </li>
        <li class="app__pagination-item">
          <a href class="app__pagination-link">4</a>
        </li>
        <li class="app__pagination-item">
          <a href class="app__pagination-link">5</a>
        </li>
      </ul>-->
    </div>
  </div>
</template>

<script>
import Movies from "./components/Movies.vue";

export default {
  name: "app",
  data() {
    return {
      keyword: "",
      movie: "",
      baseUrl: "https://api.themoviedb.org/3/",
      apiKey: "3276fa51d16eb0a7c0fcb23665588bcd",
      configData: null,
      baseImageURL: null,
      keyword: "",
      movieList: ""
    };
  },
  methods: {
    getConfig() {
      let url = "".concat(this.baseUrl, "configuration?api_key=", this.apiKey);
      fetch(url)
        .then(result => {
          return result.json();
        })
        .then(data => {
          this.baseImageURL = data.images.secure_base_url;
          this.configData = data.images;
          // console.log("Config data: ", data);
          // this.runSearch("Avengers");
        })
        .catch(function(err) {
          console.log(err);
        });
    },
    runSearch(keyword) {
      let url = "".concat(
        this.baseUrl,
        "search/movie?api_key=",
        this.apiKey,
        "&query=",
        keyword,
        "&language=pt-BR&region=BR"
      );
      fetch(url)
        .then(result => result.json())
        .then(data => {
          this.movieList = data;
          // console.log(this.movieList);
        });
    }
  },
  components: {
    appMovies: Movies
  }
};
</script>

<style>
</style>
