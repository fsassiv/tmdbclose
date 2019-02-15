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
      <div v-if="!movieList && !movieCounter">
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
          @getSingleMovie="getSingleMovie(movie.id)"
          :key="movie.id"
          v-for="movie in movieList.results"
          :opt="movie"
        ></app-movies>
      </ul>
      <!-- LOAD SINGLE RESULT -->
      <div v-if="singleMovie" class="app__single-movie">
        <appMovie :key="movie" v-for="movie in movieCounter" :opt="singleMovie"></appMovie>
      </div>
      <!-- PAGINATION -->
      <ul v-if="movieList" class="app__pagination">
        <li
          :key="page"
          v-for="page in movieList.total_pages"
          :class="{active:page==movieList.page}"
          class="app__pagination-item"
        >
          <a
            :href="page"
            @click.prevent="runSearch(keyword,page)"
            class="app__pagination-link"
          >{{page}}</a>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import Movies from "./components/Movies.vue";
import Movie from "./components/Movie.vue";

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
      movieList: [],
      movieCounter: [],
      singleMovie: "",
      movieId: ""
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
    runSearch(keyword, page = 1) {
      this.movieCounter = "";
      let url = "".concat(
        this.baseUrl,
        "search/movie?api_key=",
        this.apiKey,
        "&query=",
        keyword,
        "&language=pt-BR&region=BR&page=",
        page
      );
      fetch(url)
        .then(result => result.json())
        .then(data => {
          this.movieList = data;
          // console.log(data);
        });
    },
    getSingleMovie(movieId) {
      this.movieList = [];
      this.movieCounter = 1;
      let apiKey = "3276fa51d16eb0a7c0fcb23665588bcd";
      let url = "".concat(
        "https://api.themoviedb.org/3/movie/",
        movieId,
        "?api_key=",
        apiKey,
        "&language=pt-BR&region=BR"
      );
      fetch(url)
        .then(response => {
          return response.json();
        })
        .then(data => {
          // console.log(data);
          this.singleMovie = data;
        });
    }
  },
  components: {
    appMovies: Movies,
    appMovie: Movie
  }
};
</script>

<style>
</style>
