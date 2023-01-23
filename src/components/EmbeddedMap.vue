<template>
  <div class="map-frame">
    <p>Type de map:</p>
    <select v-model="mode">
      <option value="m">Mode route</option>
      <option value="k">Mode satellite</option>
    </select>
    <iframe :src="mapSrc" frameborder="0" scrolling="no" marginheight="0" marginwidth="0"
      class="map-container"></iframe>
  </div>
</template>
<script>
export default {
  name: "EmbeddedMap",
  props: {
    query: {
      type: String,
      default: "Place Bellecour, Lyon, France",
    },
    zoom: {
      type: Number,
      default: 2,
    },
    mapMode: {
      type: String,
      default: "m"
    }
  },
  computed: {
    mapSrc: function () {
      return `https://maps.google.com/maps?q=${this.query}&t=${this.mode}&z=${this.zoom}&ie=UTF8&iwloc=&output=embed`;
    },
  },
  data() {
    return {
      mode: ""
    }
  },
  mounted() {
    this.mode = this.mapMode;
  },
  watch: {
    mapMode: function (newMode) {
      this.mode = newMode;
    },
    mode: function (newMode) {
      this.$emit("mapModeChange", newMode);
    }
  }
};
</script>
<style scoped>

.map-frame {
  border: 1px solid white;
  background-color: white;
  padding: 20px;
}
.map-container {
  width: 100%;
  height: 500px;
}
</style>
