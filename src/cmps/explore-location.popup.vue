<template>
  <div class="location-container flex">
    <div class="popup-lt-side flex">
      <div class="lt map-header">Search by region</div>
      <div class="maps-wrapper">
        <div class="map-loc" v-for="(map, idx) in maps" :key="idx" @click="setLocation(map.loc)">
          <div class="img-con" :style="{ 'background-image': 'url(' + map.src + ')' }"> </div>
          <span>{{ map.loc }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { emitChangeFn } from 'element-plus';

export default {
  name: 'explore-maps',
  data() {
    return {
      maps: [],
    };
  },
  created() {
    return (this.maps = this.$store.getters.getMaps);
  },

  methods: {
    setLocation(loc) {
      console.log(loc);
      this.$emit('filterByMap', loc)
    }
  }
}
</script>
