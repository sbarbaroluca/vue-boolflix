<template>
  <div id="app">
    <Header 
    @genereSerieSelezionato="salvoGenereSerieSelezionato"
    @genereFilmSelezionato="salvoGenereFilmSelezionato"
    @passoQuery="salvoQuery" 
    :moviesGenre="moviesGenre"
    :seriesGenre="seriesGenre"
    />
    <Main 
    :queryString="queryString" 
    @passoGeneri="salvoGeneri"
    :genereSerieSelezionato="genereSerieSelezionato"
    :genereFilmSelezionato="genereFilmSelezionato"
    />
  </div>
</template>

<script>
import Header from "./components/Header";
import Main from "./components/Main";
export default {
  name: "App",
  components: {
    Header,
    Main
  },
  data() {
    return {
      queryString: "",
      moviesGenre: [],
      seriesGenre: [],
      genereFilmSelezionato: undefined,
      genereSerieSelezionato: undefined
    };
  },
  methods: {
    salvoQuery(queryString) {
      this.queryString = queryString;
    },
    salvoGeneri(moviesGenre, seriesGenre) {
        moviesGenre.forEach((element) => {
            this.moviesGenre.push(element);
        });
        seriesGenre.forEach((element) => {
            this.seriesGenre.push(element);
        });
    },
    salvoGenereSerieSelezionato(genereSelezionato) {
          this.genereSerieSelezionato = parseInt(genereSelezionato);
    },
    salvoGenereFilmSelezionato(genereSelezionato) {
          this.genereFilmSelezionato = parseInt(genereSelezionato);
    }
  }
};
</script>

<style lang="scss">
@import "./style/generic";
</style>
