<template>
  <nav>
    <input type="text" v-model="search" />

    <ul>
      <li
        v-for="marker in filteredMarkers"
        :key="marker.id"
        :class="{ active: selectedId === marker.id }"
        @click="$emit('menuItemClick', marker.id, marker.latLng)"
      >{{ marker.name }}</li>
    </ul>
  </nav>
</template>

<script>
export default {
  name: 'Menu',
  props: {
    markers: Array,
    selectedId: Number,
  },
  data() {
    return {
      search: '',
    }
  },
  computed: {
    filteredMarkers() {
      return this.markers.filter(element => {
        return element.name.toLowerCase().includes(this.search.toLowerCase())
      })
    },
  },
}
</script>

<style lang="scss" scoped>
nav {
  position: absolute;
  right: 2%;
  width: 300px;
  height: 90vh;
  top: 5vh;
  z-index: 1000;
  background: #ffffff;
  border-radius: 10px;
}

input {
  margin-top: 30px;
  margin-left: 20px;
}

ul {
  margin: 0;
  padding: 0;
  margin-top: 30px;
}

li {
  padding: 5px 0px 5px 20px;
  list-style: none;
  cursor: pointer;
  font-size: 18px;
  transition: all 0.2s ease-in-out;
  border: 1px dashed rgb(196, 188, 188);
  &:hover {
    color: #ffffff;
    background: rgb(196, 188, 188);
  }
  &.active {
    color: #ffffff;
    background: rgb(196, 188, 188);
  }
}
</style>
