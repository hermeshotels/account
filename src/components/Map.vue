<template lang="html">
  <div class="map-wrapper">
    <gmap-map
      :center="{lat:10, lng:10}"
      :zoom="7"
      map-type-id="terrain"
      style="width: 100%; height: 100%"
      >
      <google-cluster>
        <gmap-marker
          v-for="m in hotelCoords"
          :position="m.position"
          @mouseover="statusText = m.name"
        ></gmap-marker>
      </google-cluster>
    </gmap-map>
  </div>
</template>
<script>
  export default {
    data () {
      return {
        center: {lat: 10.0, lng: 10.0},
        hotelCoords: []
      }
    },
    mounted () {
      this.$http.get('https://api.ermeshotels.com/api/v1/hotel/active').then((response) => {
        response.body.data.forEach((hotel) => {
          console.log(hotel)
          let address = hotel.address.replace(' ', '+')
          address = address + '+'
          address = address + hotel.zip
          this.$http.get('https://maps.googleapis.com/maps/api/geocode/json?address=' + address + '&key=AIzaSyCIXOlRBntjE_i0t_RUa3_KozNfxaE7qCc')
            .then((response) => {
              this.hotelCoords.push({
                name: hotel.name,
                position: response.body.results[0].geometry.location
              })
            })
        })
      }, (error) => {
        console.log(error)
      })
    }
  }
</script>
