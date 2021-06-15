<template>
  <div id="app">
    <Header @passoQuery="salvoQuery" />
    <Main :queryString="queryString" />
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
      queryString: ""
    };
  },
  methods: {
    salvoQuery(queryString) {
      this.queryString = queryString;
    }
  }
};
</script>

<style lang="scss">
@import "./style/generic";
</style>
