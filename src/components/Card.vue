<template>
  <div class="card">
    <ul>
      <li>{{ filmObject.title }}</li>
      <li>{{ filmObject.original_title }}</li>
      <li>{{ filmObject.original_language }}</li>
      <li>{{ filmObject.vote_average }}</li>
    </ul>
  </div>    
</template>

<script>
export default {
      name: "Card",
      props: {
        filmObject: Object
      }
};
</script>

<style scoped>
.card {
  width: 200px;
  margin: 0 15px;
  height: 300px;
  background-color: red;
}
</style>