<script>
import { inject, onMounted, onBeforeUnmount } from 'vue';
export default {
  setup() {
    const mapPromise = inject('mapPromise');
    let layer;
    onMounted(async () => {
      const map = await mapPromise;
      console.log(map);
      layer = new AMap.Marker({
        position: new AMap.LngLat(121.536231, 29.847024),
        title: '北京',
      });
      map.add(layer);
    });
    onBeforeUnmount(async () => {
      const map = await mapPromise;
      map.remove(layer);
    });
    return () => null;
  },
};
</script>
