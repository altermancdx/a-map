<template>
  <div ref="mapRef" class="map-wrapper">
    <slot />
  </div>
</template>
<script setup>
import { shallowRef, onMounted, provide } from 'vue';
import { defer } from '@/utils/promise';
const mapRef = shallowRef();
const mapDefer = defer();
provide('mapPromise', mapDefer.promise);
onMounted(() => {
  const map = new AMap.Map(mapRef.value, {
    zoom: 9,
    center: [121.536231, 29.847024],
    // animateEnable: true,
    viewMode: '3D',
    pitch: 45,
    mapStyle: 'amap://styles/9ebc150f3db9fbb943bc8b1276544393',
  });
  mapDefer.resolve(map);
  map.on('click', (ev) => {
    const lnglat = ev.lnglat;
    map.setCenter(lnglat);
  });
});
</script>
<style lang="scss" scoped>
.map-wrapper {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
}
</style>
