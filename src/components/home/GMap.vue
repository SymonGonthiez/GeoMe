<template>
    <div class="map">
        <div class="google-map" id="map"></div>
    </div>
</template>

<script>
import firebase from 'firebase'

export default {
    name: 'GMap',
    data(){
        return { // data which retur an empty object inside
            lat: 53,
            lng: -2
        }
    },
    methods: {
        renderMap(){
            const map = new google.maps.Map(document.getElementById('map'), { // Second parameter is object with map data
                center: {lat: this.lat , lng: this.lng },
                zoom: 6,
                maxZoom: 15,
                minZoom: 3,
                streetViewControl: false
            })
        }
    },
    mounted(){
        // Get user geolocalisation
        if(navigator.geolocation){
            navigator.geolocation.getCurrentPosition(pos => {
                this.lat = pos.coords.latitude
                this.lng = pos.coords.longitude
                this.renderMap()
            }, (err) => {
                console.log(err)
                this.renderMap()
            }, { maximumAge: 60000, timeout: 3000})
        } else  {
            // position centre by default values
            this.renderMap()
        }
        this.renderMap()
    }
}
</script>

<style>
.google-map {
    width: 100%;
    height: 100%;
    margin: 0 auto;
    background: #ffffff;
    position: absolute;
    top:0;
    left:0;
    z-index: -1;
}
</style>