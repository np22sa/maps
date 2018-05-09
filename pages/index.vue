<template>
  <section class="container">
    <div>
      <logo/>
      <h1 class="title">
        maps
      </h1>
      <h2 class="subtitle">
        My well-made Nuxt.js project
      </h2>
      <div class="links">
        <a href="https://nuxtjs.org/" target="_blank" class="button--green">Documentation</a>
        <a href="https://github.com/nuxt/nuxt.js" target="_blank" class="button--grey">GitHub</a>
      </div>
    </div>
    <div id="map"></div>
  </section>
</template>

<script>
import Logo from '~/components/Logo.vue'

export default {
  components: {
    Logo
  },
  data () {
  return {
    mapName: "map",
    markerCoordinates: [{
      latitude: 51.501527,
      longitude: -0.1921837
    }, {
      latitude: 51.505874,
      longitude: -0.1838486
    }, {
      latitude: 51.4998973,
      longitude: -0.202432
    }],
    map: null,
      bounds: null,
      markers: []
  }
},
    mounted() {
    // const autocomplete = this.$google.maps.places.Autocomplete(inputElement,
    //   {
    //     types: ['geocode'],
    //   },
    //);
    this.bounds = new google.maps.LatLngBounds();

    const element = document.getElementById('map')
    const mapCentre = this.markerCoordinates[0];
    const options = {
      zoom: 14,
      center: new google.maps.LatLng(mapCentre.latitude, mapCentre.longitude)
    }
    this.map = new google.maps.Map(element, options);
    this.markerCoordinates.forEach((coord) => {
      const position = new google.maps.LatLng(coord.latitude, coord.longitude);
      const marker = new google.maps.Marker({ 
        position,
        map: this.map,
        title: coord.latitude+','+coord.longitude
      });
      this.markers.push(marker)
      this.map.fitBounds(this.bounds.extend(position))
    });
  },
}
</script>

<style>
       #map {
        height: 400px;
        width: 100%;
       }
.container
{
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}
.title
{
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif; /* 1 */
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}
.subtitle
{
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}
.links
{
  padding-top: 15px;
}
</style>
