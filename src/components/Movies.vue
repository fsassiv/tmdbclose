<template>
  <li class="app__movie">
    <img
      :src="'https://image.tmdb.org/t/p/w500'+posterUrl"
      alt="Image not found"
      class="app__movie-poster"
    >
    <div class="app__movie-info">
      <div class="app__movie-header">
        <h3 class="app__movie-title is-abel">
          <a
            :href="'https://www.themoviedb.org/movie/'+movieId"
            target="_blank"
            class="app__movie-link"
          >{{title}}</a>
        </h3>
        <p class="app__movie-date">{{date}}</p>
        <button class="app__movie-popularity">{{vote_average}}</button>
      </div>
      <div class="app__movie-content">{{description}}</div>
      <div class="app__movie-footer">
        <ul class="app__movie-genre-list">
          <li :key="genre" v-for="genre in genresNames" class="app__movie-genre-item">{{genre}}</li>
        </ul>
      </div>
    </div>
  </li>
</template>

<script>
//image.tmdb.org/t/p/w300_and_h450_bestv2/1YxnYKJaY3oIdqdOBw8uh7Bb2gI.jpg
// get config data
//api.themoviedb.org/3/configuration?api_key=apiKey

// fetch databased on keyword
//api.themoviedb.org/3/search/movie?api_key=apiKey&query=KEYWORD

// Details about one movie
//api.themoviedb.org/3/movie/movieId?api_key=apiKey
export default {
  props: {
    movieId: Number,
    posterUrl: String,
    title: String,
    date: String,
    vote_average: Number,
    description: String,
    genres: Array
  },
  data() {
    return {
      genresNames: []
    };
  },
  methods: {
    getDrama() {
      let apiKey = "3276fa51d16eb0a7c0fcb23665588bcd";
      let url = "".concat(
        "https://api.themoviedb.org/3/movie/",
        this.movieId,
        "?api_key=",
        apiKey
      );
      fetch(url)
        .then(response => {
          return response.json();
        })
        .then(data => {
          this.getGenreName(data.genres);
        });
    },
    getGenreName(genreList) {
      // console.log(genreList);
      // console.log(this.genres);
      let newGenreList = [];
      let i;
      for (i in genreList) {
        newGenreList.push(genreList[i].name);
      }
      this.genresNames = newGenreList;
    }
  },
  mounted() {
    this.getDrama();
  }
};
</script>

<style>
</style>
