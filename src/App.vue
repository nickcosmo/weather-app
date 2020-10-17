<template>
  <div>
    <h1>Whats The Weather?</h1>
  </div>
  <div>
    <input type="text" v-model="cityName">
    <button @click='fetchData'>Get Weather!</button>
  </div>
  <weather v-bind:temperature="temperature"></weather>
</template>

<script>
import Weather from './components/Weather.vue';

export default {
  data() {
    return {
      temperature: null,
      cityName: '',
    }
  },
  methods: {
    fetchData() {
      let temp = 0;
      fetch(`http://api.openweathermap.org/data/2.5/weather?q=${this.cityName}&appid=35ee102ebd52c46e68e293c39d139fe3`)
        .then(res => res.json())
        .then(weatherData => {temp = weatherData.main.temp
           this.temperature = Math.floor(temp - 273.15);
        });
      return this.temperature;
    }
  },
  components: {
    Weather
  }
}
</script>

<style>
html {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  background-color: black;
  font-family: sans-serif;
}

div {
  margin-top: 30px;
  width: 100%;
  text-align: center;
  color: white;
  font-size: 50px;
}

button {
  background-color: white;
  font-size: 20px;
  padding: 5px 4px;
  border: none;
  font-family: Arial;
  text-decoration: none;
  display: inline-block;
  color: black;
  cursor: pointer;
  outline: none;
  margin-left: 5px;
  /* transition: 0.5s ease-in-out; */
}

button:hover {
  /* background-color: black;
  color: white; */
  animation: bump 0.2s ease-out;
}

input {
  background-color: white;
  padding: 5px 4px;
  border: none;
  font-family: Arial;
  text-decoration: none;
  display: inline-block;
  color: black;
  outline: none;
  font-size: 20px;
}

.v-enter.active {

}

@keyframes bump {
  0% {
    transform: translateY(0);
  }

  50% {
    transform: translateY(-10px);
  }

  70% {
    transform: translateY(+3px);
  }

  100% {
    transform: translateY(0%);
  }
}
</style>
