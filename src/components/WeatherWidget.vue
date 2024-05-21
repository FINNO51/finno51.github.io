<template>
  <div class="container">
    <!--
    <div class="header">
      <div class="search-bar">
        <input
          type="text"
          v-model="city"
          placeholder="Enter city name"
          class="search-input"
        />
        <button @click="searchByCity" class="search-button">Search</button>
      </div>
    </div>
-->
    <main class="main-section">
      <Transition :duration="550" name="nested" mode="out-in">
        <div v-if="weatherData" class="weather">
          <div class="inner">
            <h2>{{ weatherData.name }}, {{ weatherData.sys.country }}</h2>
            <div class="temp-box">
              <div class="time">{{ currentTime }}</div>
              <img :src="iconUrl" class="weather-icon" />
              <div class="temperature">{{ temperature }} °C</div>
            </div>
          </div>
        </div>
        <div v-else class="weather" :style="{ height: '6rem' }">
          <div class="inner"><h2>Cargando...</h2></div>
        </div>
      </Transition>
    </main>
  </div>
</template>

<script>
import axios from "axios";

const apikey = "6ae63a9a797d216794285e7d1474ba92";

export default {
  name: "App",
  data() {
    return {
      city: "",
      weatherData: null,
      d: new Date(),
    };
  },
  computed: {
    temperature() {
      return this.weatherData
        ? Math.floor(this.weatherData.main.temp - 273)
        : null;
    },
    iconUrl() {
      return this.weatherData
        ? `http://api.openweathermap.org/img/w/${this.weatherData.weather[0].icon}.png`
        : null;
    },
    currentTime() {
      let currentHours = this.d.getHours();
      currentHours = ("0" + currentHours).slice(-2);
      let currentMinutes = this.d.getMinutes();
      currentMinutes = ("0" + currentMinutes).slice(-2);
      return currentHours + ":" + currentMinutes;
    },
  },
  mounted() {
    this.fetchCurrentLocationWeather();
    this.getTime();
    let that = this;
    setInterval(function () {
      that.fetchCurrentLocationWeather();
      that.getTime();
    }, 1000);
  },
  methods: {
    async fetchCurrentLocationWeather() {
      if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition(async (position) => {
          const { latitude, longitude } = position.coords;
          const url = `http://api.openweathermap.org/data/2.5/weather?lat=${latitude}&lon=${longitude}&appid=${apikey}`;
          await this.fetchWeatherData(url);
        });
      }
    },
    async fetchWeatherData(url) {
      try {
        const response = await axios.get(url);
        this.weatherData = response.data;
      } catch (error) {
        console.error("Error fetching weather data:", error);
      }
    },
    async searchByCity() {
      if (!this.city) return;
      try {
        const urlsearch = `http://api.openweathermap.org/data/2.5/weather?q=${this.city}&appid=${apikey}`;
        const response = await axios.get(urlsearch);
        this.weatherData = response.data;
        this.getTime();
      } catch (error) {
        console.error("Error fetching weather data:", error);
      }
      this.city = "";
    },
    async getTime() {
      if (this.weatherData) {
        let localTime = this.d.getTime();
        let localOffset = this.d.getTimezoneOffset() * 60000;
        let utc = localTime + localOffset;
        let cityTime = utc + 1000 * this.weatherData.timezone;
        this.d = new Date(cityTime);
      }
    },
  },
};
</script>

<style scoped>
.container {
  display: flex;
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem;
  height: 20rem;
  align-items: center;
}

.main-section {
  display: flex;
  align-items: center;
}

/* Header */
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 2rem;
}

.header h1 {
  font-family: "Orbitron", sans-serif;
  font-size: 2.5rem;
  color: #2b6cb0;
  margin: 0;
}

/* Search Bar */
.search-bar {
  display: flex;
  align-items: center;
  margin-bottom: 2rem;
}

.search-input {
  font-size: 1rem;
  padding: 0.5rem;
  border: 1px solid #ccc;
  border-radius: 0.25rem;
  background-color: #f5f5f5;
  width: 60%;
  margin-right: 1rem;
}

.search-button {
  font-size: 1rem;
  background-color: #4a90e2;
  color: white;
  border: none;
  border-radius: 0.25rem;
  padding: 0.5rem 1rem;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.search-button:hover {
  background-color: #357dbf;
}

/* Weather Widget */
.weather {
  display: flex;
  flex-direction: column;
  text-align: left;
  color: #fff;
  min-height: 6rem;
  width: 22rem;
  padding: 2rem;
  background-color: var(--color-border);
  border-radius: 1rem;
  box-shadow: 0px 0px 15px 0px rgba(0, 0, 0, 0.1);
}

.weather h2 {
  font-size: 1.2rem;
  font-weight: 500;
  margin-bottom: 0.4rem;
  color: var(--color-heading);
}

.temp-box {
  display: flex;
  flex-direction: row;
  align-items: center;
}

.weather-icon {
  width: 60px;
  height: 60px;
  border-radius: 50%;
  background-color: var(--color-border-hover);
}

.temperature {
  font-size: 2rem;
  height: 2rem;
  line-height: 1.5rem;
  padding-left: 1.5rem;
}

.time {
  font-size: 2rem;
  height: 2rem;
  line-height: 1.5rem;
  padding-right: 1.5rem;
}
</style>
