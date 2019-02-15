<template>
  <div class="app__single">
    <div class="app__single-header bg-grey">
      <h1 class="app__single-title is-abel">{{opt.title}}</h1>
      <span class="app__single-date">{{opt.release_date}}</span>
    </div>
    <div class="app__single-content">
      <div class="app__single-info">
        <section class="app__single-section">
          <h3 class="app__single-subtitle">Sinopse</h3>
          <p class="app__single-text">{{opt.overview}}</p>
        </section>
        <section class="app__single-section">
          <h3 class="app__single-subtitle">Informações</h3>
          <ul class="app__single-details">
            <li class="app__single-detail">
              <p class="app__single-label">Situação</p>
              <p class="app__single-value">{{opt.sit}}</p>
            </li>
            <li class="app__single-detail">
              <p class="app__single-label">Idioma</p>
              <p class="app__single-value">
                <span :key="l.id" v-for="l in opt.spoken_languages">{{l.name}},</span>
              </p>
            </li>
            <li class="app__single-detail">
              <p class="app__single-label">Duração</p>
              <p class="app__single-value">{{opt.runtime}} minutos</p>
            </li>
            <li class="app__single-detail">
              <p class="app__single-label">Orçamento</p>
              <p class="app__single-value">{{opt.budget}}</p>
            </li>
            <li class="app__single-detail">
              <p class="app__single-label">Receita</p>
              <p class="app__single-value">{{opt.revenue}}</p>
            </li>
            <li class="app__single-detail">
              <p class="app__single-label">Lucro</p>
              <p class="app__single-value">{{opt.revenue - opt.budget}}</p>
            </li>
          </ul>
        </section>
        <section class="app__single-section rel">
          <ul class="app__movie-genre-list">
            <li
              :key="genre.id"
              v-for="genre in opt.genres"
              class="app__movie-genre-item"
            >{{genre.name}}</li>
            <button class="app__movie-popularity bigger">{{opt.popularity}}</button>
          </ul>
        </section>
      </div>
      <div class="app__single-poster">
        <img
          :src="'https://image.tmdb.org/t/p/w500'+opt.poster_path"
          alt
          class="app__single-poster-img"
        >
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    opt: {}
  },
  data() {
    return {};
  }
};
</script>

<style>
</style>
