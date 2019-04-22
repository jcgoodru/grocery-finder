<template>
  <div id="app" class="container">
    <div class="row">
      <div class="col-12">
        <h1>Healthy Choices</h1>
      </div>
    </div>
    <MapSearch/>
  </div>
</template>

<script>
import MapSearch from '@/components/MapSearch.vue';

export default {
  name: 'app',
  components: {
    MapSearch,
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
