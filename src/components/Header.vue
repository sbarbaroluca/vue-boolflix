<template>
  <header class="d-flex">
    <div class="logo-img">
      <img src="../assets/images/logo.png" alt="Gianflix" />
    </div>
    <div class="from">
      <Searchbar 
          @passoQuery="passoQuery"
          @genereSerieSelezionato="genereSerieSelezionato"
          @genereFilmSelezionato="genereFilmSelezionato"
          :moviesGenre="moviesGenre"
          :seriesGenre="seriesGenre"
       />
    </div>    
  </header>
</template>

<script>
import Searchbar from "./Searchbar";
export default {
      name: "Header",
      components: {
          Searchbar
      },
      props: {
          moviesGenre: Array,
          seriesGenre: Array
      },
      methods: {
        passoQuery(queryString) {
          this.$emit("passoQuery", queryString);
        },
        genereSerieSelezionato(genereSerieSelezionato) {
          this.$emit("genereSerieSelezionato", genereSerieSelezionato);
        },
        genereFilmSelezionato(genereFilmSelezionato) {
          this.$emit("genereFilmSelezionato", genereFilmSelezionato);
        }
      }
};
</script>

<style lang="scss" scoped>
@import "../style/variables";
header {
    position: fixed;
    z-index: 10;
    height: $headerHeight;
    width: 100%;
    padding: 0 1%;
    justify-content: space-between;
    background-color: $netflixGrey;
    img {
      height: 100%;
    }
    .from {
      align-self: center;
      display: flex;
      width: 100%;
    }
}
</style>