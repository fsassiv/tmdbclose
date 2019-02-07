<template>
  <div class="app__single">
    <div class="app__single-header bg-grey">
      <h1 class="app__single-title is-abel">{{title}}</h1>
      <span class="app__single-date">{{date}}</span>
    </div>
    <div class="app__single-content">
      <div class="app__single-info">
        <section class="app__single-section">
          <h3 class="app__single-subtitle">Sinopse</h3>
          <p class="app__single-text">{{sinopse}}</p>
        </section>
        <section class="app__single-section">
          <h3 class="app__single-subtitle">Informações</h3>
          <ul class="app__single-details">
            <li class="app__single-detail">
              <p class="app__single-label">Situação</p>
              <p class="app__single-value">{{sit}}</p>
            </li>
            <li class="app__single-detail">
              <p class="app__single-label">Idioma</p>
              <p class="app__single-value">
                <span :key="l.id" v-for="l in lang">{{l.name}},</span>
              </p>
            </li>
            <li class="app__single-detail">
              <p class="app__single-label">Duração</p>
              <p class="app__single-value">{{dur}} minutos</p>
            </li>
            <li class="app__single-detail">
              <p class="app__single-label">Orçamento</p>
              <p class="app__single-value">{{budget}}</p>
            </li>
            <li class="app__single-detail">
              <p class="app__single-label">Receita</p>
              <p class="app__single-value">{{total}}</p>
            </li>
            <li class="app__single-detail">
              <p class="app__single-label">Lucro</p>
              <p class="app__single-value">{{total - budget}}</p>
            </li>
          </ul>
        </section>
        <section class="app__single-section rel">
          <ul class="app__movie-genre-list">
            <li :key="genre.id" v-for="genre in genres" class="app__movie-genre-item">{{genre.name}}</li>
            <button class="app__movie-popularity bigger">{{popularity}}</button>
          </ul>
        </section>
      </div>
      <div class="app__single-poster">
        <img :src="'https://image.tmdb.org/t/p/w500'+posterUrl" alt class="app__single-poster-img">
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    movieId: "",
    title: "",
    posterUrl: "",
    date: "",
    sinopse: "",
    sit: "",
    dur: "",
    budget: "",
    total: "",
    profit: "",
    popularity: "",
    genres: Array,
    lang: Array
  },
  data() {
    return {};
  }
};
</script>

<style>
</style>
