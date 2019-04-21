<template>
  <div>
    <h1>Closest Stores</h1>
    <div class="d-flex justify-content-between p-2" v-for="store in stores" :key="store.id">
      <div>
        <span class="heavy-text pr-2">{{ store.name }}</span>
        <span class="light-text">0.4 mi</span>
      </div>
      <div class="d-flex">
        <div v-if="store.produce"><i class="fas fa-apple-alt"></i></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      stores: [
        {
          id: 1,
          lat: 42.9,
          lon: -78.0,
          name: 'Tops',
          produce: true
        },
        {
          id: 2,
          lat: 42.9,
          lon: -78.0,
          name: 'Holley Farms',
          produce: false
        },
        {
          id: 3,
          lat: 42.95,
          lon: -78.1,
          name: 'PriceRite',
          produce: true
        },
      ]
    }
  }
}
</script>

<style>
.heavy-text {
  font-weight: bold;
}
.light-text {
  color: #999;
  font-size: 80%;
}
</style>
