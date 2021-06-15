<template>
  <main class="p-5 container-fluid">
    <h2 class="text-center mb-5">Movies</h2>
    <div class="row justify-content-center">
      <div class="col-2" v-for="(movie, index) in movies" :key="movie.id">
      <Card 
        :datas="movies[index]"
        titleKey="title"
        originalTitleKey="original_title"
      />
      </div>
    </div>
    <h2 class="text-center m-5">Series</h2>
    <div class="row justify-content-center">
      <div class="col-2" v-for="(serie, index) in series" :key="serie.id">  
      <Card 
        :datas="series[index]"
        titleKey="name"
        originalTitleKey="original_name"
      />
      </div>
    </div>  
  </main>    
</template>

<script>
import axios from "axios";
import Card from "./Card";
export default {
        name: "Main",
        components: {
            Card
        },
        data() {
          return {
            movies: {},
            series: {}
          };
        },
        props: {
          queryString: String
        },
        watch: {
          queryString: function (val) {
            const getMovies = () =>
              axios.get("https://api.themoviedb.org/3/search/movie/", {
                    params: {
                        api_key: "d008764413ef1bbe6d3e652a2f6eb22e",
                        language: "it-IT",
                        query: val
                    }
                  });
            const getSeries = () =>
              axios.get("https://api.themoviedb.org/3/search/movie/", {
                    params: {
                        api_key: "d008764413ef1bbe6d3e652a2f6eb22e",
                        language: "it-IT",
                        query: val
                    }
                  });      
            Promise.all([getMovies(), getSeries()]).then((res) => {
                this.movies = res[0].data.results;
                this.series = res[1].data.results;
            });
          }
      },
      methods: {}
};            
</script>

<style lang="scss" scoped>
@import "../style/variables";
main {
    flex-wrap: wrap;
    min-height: calc(100vh - #{$headerHeight});
    .row {
          & > [class*="col"] {
                margin-left: 1%;
          }
    }
}
</style>