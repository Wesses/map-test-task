<template>
  <div class="text-center">
    <NavBar />
    <MapPage />
  </div>
</template>

<script>
import NavBar from './components/NavBar.vue';
import MapPage from './components/MapPage.vue'

export default {
  name: 'App',
  components: {
    NavBar,
    MapPage,
  }
}
</script>
