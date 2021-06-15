<template>
  <main class="p-5">
      <Card 
        :filmObject="filmObject.results[index]"
        v-for="(film, index) in filmObject.results"
        :key="index"
      />
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
            filmObject: {}
          };
        },
        props: {
          queryString: String
        },
        watch: {
          queryString: function (val) {
            axios
                  .get("https://api.themoviedb.org/3/search/movie/", {
                    params: {
                        api_key: "d008764413ef1bbe6d3e652a2f6eb22e",
                        language: "it-IT",
                        query: val
                    }
                  })
                  .then((res) => {
                    this.filmObject = res.data;
                  });
          }
        },
        methods: {}
};
</script>

<style lang="scss" scoped>
@import "../style/variables";
main {
    min-height: calc(100vh - #{$headerHeight});
    background-color: grey;
}
</style>