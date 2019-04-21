<template>
  <div id="app" class="container">
    <div class="row">

      <!-- Header -->
      <div class="col-12">
        <h1>Header</h1>
      </div>

      <!-- Map and Search -->
      <div class="col-12 col-lg-6">
        <MapSearch/>
      </div>

      <!-- Search Results -->
      <div class="col-12 col-lg-6">
        <SearchResults/>
      </div>

    </div>
  </div>
</template>

<script>
import MapSearch from '@/components/MapSearch.vue';
import SearchResults from '@/components/SearchResults.vue';

export default {
  name: 'app',
  components: {
    MapSearch,
    SearchResults
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
