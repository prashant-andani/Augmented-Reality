<template>
<a-scene id="scene" embedded arjs='sourceType: webcam;'>    
  <a-marker v-for="marker in markers" :key="marker.id" type="pattern" preset='custom' 
  v-bind:patternUrl="marker.url" v-bind:url="marker.url"> 
    <a-plane position="0 -0.05 0" rotation="-60 0 0" width="1" height="1" v-bind:color="marker.color">
        <a-text value="Conference Room" width="2.5" height="2.5" position='-0.4 0.4 0' material="align:center" color="#ffffff"></a-text>
        <a-text v-bind:value="marker.roomName" width="3" height="3" position='-0.4 0.25 0' material="align:center" color="#ffffff"></a-text>
        <a-text v-bind:value="marker.status" width="2" height="2" position='-0.4 0.15 0' material="align:center" color="#ffffff"></a-text>
        <a-text v-bind:value="marker.info" width="1.6" height="1" position='-0.4 0.02 0' material="align:center" color="#ffffff"></a-text>
      <a-text>
      
      </a-text>
    </a-plane>
  </a-marker>
  <a-entity camera></a-entity>
  </a-scene>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      markers: [
      {
        id: 1,
        roomName: 'Mahabodhi',
        url: './src/assets/pattern-letterA.patt',
        status: 'Available',
        info: 'for next 30 mins',
        color: '#4B77BE',
      },
      {
        id: 2,
        roomName: 'Tulip (Room)',
        url: './src/assets/pattern-letterB.patt',
        status: 'Not Available',
        info: 'for next 2 Hours',
        color: '#6C7A89'
      },
      {
        id: 3,
        roomName: 'Lotus (Room)',
        url: './src/assets/pattern-letterC.patt',
        status: 'Available',
        info: 'for next 1 Hour',
        color: '#BDC3C7'
      },
      {
        id: 4,
        roomName: 'Hibiscus (Room)',
        url: './src/assets/pattern-letterD.patt',
        status: 'Not Available',
        info: 'for next 2 mins',
        color: '#D35400'
      },
      { 
        id: 5,
        roomName: 'Jasmine (Room)',
        url: './src/assets/pattern-letterF.patt',
        status: 'Available',
        info: 'for next 24 Hours',
        color: '#1E824C'
      },
      {
        id: 6,
        roomName: 'Daffodil (Room)',
        url: './src/assets/pattern-letterG.patt',
        status: 'Not Available',
        info: 'for next 10 mins',
        color: '#1E824C'
      },
    ]
    }
  },
  methods: {
    getWeather() {
      let url = 'http://samples.openweathermap.org/data/2.5/weather?';
      const apiId = 'c20c0d18c636cc1463f50a40769f1b5f';
      let lat, long;
      if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition(function(pos){
          lat = pos.coords.latitude;
          long = pos.coords.longitude;
          url = url + 'lat=' + lat + '&lon=' + long + '&appid=' + apiId;
          fetch(url, {mode: 'no-cors'}).then(function(response) {
            console.log(response.data);
          });
        });
      }

    }
  },
  mounted () {
    this.getWeather();
  }
  
}
</script>
