<template>
  <div class="relative w-full h-[calc(100vh-77px)]">
    <a 
      href="https://www.maptiler.com" 
      class="absolute left-2.5 bottom-2.5 z-99"
    >
      <img 
        src="https://api.maptiler.com/resources/logo.svg" 
        alt="MapTiler logo"
      >
    </a>
    <div 
      class="absolute w-full h-full" 
      ref="mapContainer" 
    />
    <pre id="info" />
  </div>
</template>

<script>
import { Map, NavigationControl, Marker } from 'maplibre-gl';
import { shallowRef, onMounted, onUnmounted, markRaw } from 'vue';

export default {
  name: "MapPage",
  setup() {
    const mapContainer = shallowRef(null);
    const map = shallowRef(null);

    onMounted(() => {
      const apiKey = 'GNfV8yFdRo36yY1JVT21';

      const initialState = { lng: 30.52415821153156, lat: 50.44569258705531, zoom: 14 };

      map.value = markRaw(new Map({
        container: mapContainer.value,
        style: `https://api.maptiler.com/maps/streets-v2/style.json?key=${apiKey}`,
        center: [initialState.lng, initialState.lat],
        zoom: initialState.zoom
      }));

      map.value.addControl(new NavigationControl(), 'top-right');
      new Marker({ color: "#FF0000" })
        .setLngLat([139.7525, 35.6846])
        .addTo(map.value);

      map.value.on('click', (e) => {
        console.log(document.getElementById('info').innerHTML =
          `${JSON.stringify(e.point)} ${JSON.stringify(e.lngLat.wrap())}`);
      });

    }),
      onUnmounted(() => {
        map.value?.remove();
      })

    return {
      map, mapContainer
    };
  }
};
</script>
<style scoped>
@import 'maplibre-gl/dist/maplibre-gl.css';
</style>