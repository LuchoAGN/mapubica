<template>
  <div class="home">
    <l-map
    :zoom="zoom"
    :center="center"
    >
      <l-tile-layer :url="url">
      </l-tile-layer>
      <l-control-layers/>
      <l-marker v-for="provider in providers" :key="provider.name"
        :lat-lng="[provider.location.latitude, provider.location.longitude]">
        <l-icon
          :icon-url="icon"
          :icon-size="size"
        />
        <l-popup>
          <h1>{{provider.name}}</h1>
        </l-popup>
        </l-marker>
    </l-map>
  </div>
</template>

<script>
// @ is an alias to /src
import {
  LMap, LTileLayer, LControlLayers, LMarker, LPopup, LIcon,
} from 'vue2-leaflet';
import MapsEducativas from '../../../../Places/MapsEducativas';

const validME = MapsEducativas.filter(
  (MapsEducativa) => MapsEducativa.location.latitude && MapsEducativa.location.longitude,
);

export default {
  name: 'Home',
  components: {
    LMap,
    LTileLayer,
    LControlLayers,
    LMarker,
    LPopup,
    LIcon,
  },
  data() {
    return {
      providers: validME,
      zoom: 13,
      url: 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',
      center: [8.74798, -75.88143],
      icon: 'https://i.ibb.co/7nhSPxn/market.png',
      size: [35, 35],
    };
  },
};
</script>

<style lang="scss">
  .home{
    width: 100%;
    height: 100%;
}
</style>
