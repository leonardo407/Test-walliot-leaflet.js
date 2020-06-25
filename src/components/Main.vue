<template>
  <div class="wrapper" style="position: relative;">
    <l-map
      style="height: 100vh"
      :zoom="zoom"
      @update:zoom="zoomUpdated"
      :center="center"
      @update:center="centerUpdated"
    >
      <l-tile-layer :url="url"></l-tile-layer>
      <l-marker :lat-lng="marker.latLng" v-for="marker in markers" :key="marker.id">
        <l-icon>
          <img
            :src="selectedId === marker.id ? require('@/assets/images/image1.png') : require('@/assets/images/image5.png')"
          />
        </l-icon>
      </l-marker>
    </l-map>

    <Menu :markers="markers" :selectedId="selectedId" @menuItemClick="selectMarker" />
  </div>
</template>

<script>
import { LMap, LTileLayer, LMarker, LIcon } from 'vue2-leaflet'
import Menu from './Menu'

export default {
  name: 'Main',
  components: {
    LMap,
    LTileLayer,
    LMarker,
    LIcon,
    Menu,
  },
  data() {
    return {
      markers: [
        {
          id: 1,
          latitude: 50.760918,
          longitude: 4.11017,
          name: 'ВАЗ',
        },
        {
          id: 2,
          latitude: 47.492647,
          longitude: 19.051399,
          name: 'ГАЗель',
        },
        {
          id: 3,
          latitude: 41.902689,
          longitude: 12.496176,
          name: 'Lexus',
        },
        {
          id: 4,
          latitude: 43.779787,
          longitude: 11.265817,
          name: 'Volkswagen',
        },
        {
          id: 5,
          latitude: 52.373057,
          longitude: 4.892557,
          name: 'Lada',
        },
        {
          id: 6,
          latitude: -22.90315,
          longitude: -43.189903,
          name: 'Kia',
        },
        {
          id: 7,
          latitude: 38.716174,
          longitude: -9.141589,
          name: 'Bentli',
        },
        {
          id: 8,
          latitude: 50.080293,
          longitude: 14.428983,
          name: 'Porche',
        },
        {
          id: 9,
          latitude: 48.856663,
          longitude: 2.351556,
          name: 'BMW',
        },
        {
          id: 10,
          latitude: 45.438095,
          longitude: 12.319029,
          name: 'Honda',
        },
      ],

      selectedId: null,
      url: 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',
      zoom: 2,
      center: [45.438095, 12.319029],
      transtitionClosed: true,
    }
  },
  created() {
    this.markers.map(marker => {
      const mas = []
      mas.push(marker.latitude)
      mas.push(marker.longitude)

      marker.latLng = mas
    })
  },
  methods: {
    selectMarker(id, latLng) {
      if (this.transtitionClosed) {
        this.transtitionClosed = false

        this.selectedId = id
        this.center = latLng

        setTimeout(() => {
          this.zoom = 10
        }, 0)

        setTimeout(() => {
          this.center = latLng
          this.transtitionClosed = true
        }, 400)
      }
    },
    zoomUpdated(zoom) {
      this.zoom = zoom
    },
    centerUpdated(center) {
      this.center = center
    },
  },
}
</script>
