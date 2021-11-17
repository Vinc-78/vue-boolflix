<template>
  <div class="container">
    <div class="input-group justify-content-center py-5">
      <input
        type="text"
        class="w-50 fs-2"
        placeholder="Cosa vuoi cercare..."

        v-model="query"
        @keyup.enter="
          ricerca('search/movie', query, 'movies');
          ricerca('search/tv', query, 'series');
        "
      />

      <button
        class="btn btn-outline-secondary fs-2"
        type="button"

        @click="
          ricerca('search/movie', query, 'movies');
          ricerca('search/tv', query, 'series');
        "
      >
        Trova
      </button>
    </div>

    <div class="row align-items-start">
      <div class="col">
        <h2 class="py-2">Film Trovati</h2>

        <ul  v-for="movie in movies" :key="movie.id">
          <SingolCard
            :titolo="movie.title"
            :titoloOriginale="movie.original_title"
            :lingua="movie.original_language"
            :voto="movie.vote_average"
          >
          </SingolCard>
        </ul>
      </div>
      <div class="col">
        <h2 class="py-2">Serie Trovate</h2>

        <ul  v-for="serie in series" :key="serie.id">
          <SingolCard
            :titolo="serie.name"
            :titoloOriginale="serie.original_name"
            :lingua="serie.original_language"
            :voto="serie.vote_average"
          >
          </SingolCard>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import SingolCard from "./SingolCard.vue";

export default {
  name: "CardContainer",

  components: { SingolCard },

  data() {
    return {
      url: "https://api.themoviedb.org/3/",
      api_key: "8a86c3952094b7a659a25e6d8a64f76e",
      query: "",
      language: "it",
      movies: [],
      series: [],
    };
  },

  methods: {
    ricerca(url_tipo, query, dataArray) {
      axios
        .get(this.url + url_tipo, {
          params: {
            api_key: this.api_key,
            query: query,
            language: this.language,
          },
        })
        .then((ele) => {
          this[dataArray] = ele.data.results;
        });
    },
  },
  /* mounted() {
    //carico i film dalla ricerca in array muvies
    this.ricerca("search/movie", this.query, "movies");

    //carico le serie dalla ricerca in array serie

    this.ricerca("search/tv", this.query, "series");
  }, */
};
</script>