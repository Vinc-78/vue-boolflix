<template>
  <div class="container">
    <div class="input-group justify-content-end py-5">
      <input
        type="text"
        class="w-50 fs-2"
        placeholder="Cosa vuoi cercare..."
        v-model="testo"
        @keyup.enter="
          ricerca('search/movie', testo, 'movies');
          ricerca('search/tv', testo, 'series');
        "
      />

      <button
        class="btn btn-outline-secondary fs-2"
        type="button"
        @click="
          ricerca('search/movie', testo, 'movies');
          ricerca('search/tv', testo, 'series');
        "
      >
        Trova
      </button>
    </div>
    <h1 class="py-4 fs-1 fw-bold">Film Trovati</h1>
    <div class="row row-cols-3" >

      
      <div class="col g-3" v-for="movie in movies " :key="movie.id">
        

        <SingolCard 
          
          :titolo="movie.title"
          :titoloOriginale="movie.original_title"
          :paese="movie.original_language"
          :lingua="langFlags[movie.original_language]"
          :voto="movie.vote_average"
          :cover="movie.poster_path"
        >
        </SingolCard>


      </div>

    </div>

    <h1 class="py-4 fs-1 fw-bold">Serie Trovate</h1>

     <div class="row row-cols-3" >

      
      <div class="col g-3" v-for="serie in series" :key="serie.id">

        <SingolCard 
          :titolo="serie.name"
          :titoloOriginale="serie.original_name"
          :paese="serie.original_language"
          :lingua="langFlags[serie.original_language]"
          :voto="serie.vote_average"
          :cover="serie.poster_path"
        >
        </SingolCard>
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
      testo: "",
      language: "it",
      movies: [],
      series: [],
      langFlags: {
        en: "en.png",
        it: "it.png",
      },
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