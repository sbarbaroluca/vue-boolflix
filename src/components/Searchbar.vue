<template>
  <from class="row g-3">
      <Select 
            class="col-auto"
            :datas="seriesGenre"
            @passoGenereSelezionato="genereSerieSelezionato"
            msg="Filtra il genere delle serie Tv"
            firstOption="Tutte le serie"
      />  
      <Select 
            class="col-auto"
            :datas="moviesGenre"
            @passoGenereSelezionato="genereFilmSelezionato"
            msg="Filtra il genere dei Film"
            firstOption="Tutti i film"
      />  
      <div class="col-auto">
        <input 
        type="text" 
        class="from-control" 
        placeholder="Inserisci titolo" 
        v-model="queryString"
        />
      </div>
      <div class="col-auto">
        <button 
        type="submit" 
        class="btn btn-primary" 
        @click.prevent="$emit('passoQuery', queryString)"
        >
          Ricerca
        </button>  
      </div>
  </from>
</template>

<script>
import Select from "./Select";
export default {
        name: "Searchbar",
        components: {
          Select
        },
        props: {
          moviesGenre: Array,
          seriesGenre: Array
        },
        data() {
          return {
            queryString: ""
          };
        },
        methods: {
          genereSerieSelezionato(genereSerieSelezionato) {
            this.$emit("genereSerieSelezionato", genereSerieSelezionato);
          },
          genereFilmSelezionato(genereFilmSelezionato) {
            this.$emit("genereFilmSelezionato", genereFilmSelezionato);
          }
        }
};
</script>

<style scoped>
from {
  width: 100%;
  justify-content: flex-end;
  align-items: center;
}
</style>