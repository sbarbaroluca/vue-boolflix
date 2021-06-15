<template>
  <from class="row g-3">
      <div class="col-auto">
        <input type="text" class="from-control" placeholder="Input" v-model="queryString" />
      </div>
      <div class="col-auto">
        <button type="submit" class="btn btn-primary" @click.prevent="$emit('passoQuery', queryString)">
          BAMBINI
        </button>  
      </div>
  </from>
</template>

<script>
export default {
        name: "Searchbar",
        data() {
          return {
            queryString: ""
          };
        }
};
</script>

<style scoped>

</style>