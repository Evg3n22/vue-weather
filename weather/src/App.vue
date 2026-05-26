<script>

export default {
  data() {
    return {
      location: '',
      temperature: 0 | null,
      weather: '',
      loading: false,
      error: false,
      searchQuery: '',
    }
  },
  computed: {
    weatherClass() {
      if (this.weather.includes('Sunny')) {
        return 'sunny';
      } else if (this.weather.toLowerCase().includes('rain')) {
        return 'rainy';
      } else if (this.weather.toLowerCase().includes('cloudy')) {
        return 'cloudy';
      } else {
        return '';
      }
    }
  },
  methods: {
    weatherSearch() {
      this.loading = true;
      this.error = false;
      // d46a4caa73b2464688f155105262605
      fetch(`http://api.weatherapi.com/v1/current.json?key=d46a4caa73b2464688f155105262605&q=${this.searchQuery}`)
        .then(res => res.json())
        .then(data => {
          this.loading = false;
          this.location = data.location.name;
          this.temperature = data.current.temp_c;
          this.weather = data.current.condition.text;
          this.resetSearchQuery();
        })
        .catch(err => {
          this.loading = false;
          this.error = true;
          console.error(err);
        })
    },

    resetSearchQuery() {
      this.loading = false;
      this.searchQuery = '';
    }
  },

}

</script>

<template>
  <div class="weather" :class="weatherClass">
    <div class="container">

      <div class="card weather-form">
        <input type="text" placeholder="Enter city name" 
        class="weather-input__form" v-model="searchQuery" @keyup.enter="weatherSearch">
        <button class="weather-form__btn" @click="weatherSearch">Search</button>
      </div>

      <div class="card weather-load" v-if="loading">Loading...</div>

      <div class="weather-info" v-show="!error && location && temperature !== null && weather">

        <div class="card" v-if="error">Error</div>

        <div class="weather-info__text">
          <p class="card">{{ location }}</p>
          <p class="card">{{ temperature }} C</p>
          <p class="card">{{ weather }}</p>
        </div>
      </div>

    </div>
    

    <div class="weather-bg">
      <div>
        <img class="weather-bg__img bg" src="./assets/bg.jpg" alt="bg">
        <img class="weather-bg__img sunny" src="./assets/sunny.jpg" alt="sunny">
        <img class="weather-bg__img rainy" src="./assets/rainy.jpg" alt="rainy">
        <img class="weather-bg__img cloudy" src="./assets/cloudy.webp" alt="cloudy">
      </div>
    </div>
  </div>
</template>
