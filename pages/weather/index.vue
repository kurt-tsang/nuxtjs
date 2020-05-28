<template>
  <div class="container">
    <div>
      <logo />
      <h1 class="title">
        nuxtjs
      </h1>
      <h2 class="subtitle">
        My astonishing Nuxt.js project - Version 2.1
      </h2>
      <div class="links">
        <input type="text" v-model="city" />
        <button
          class="button--green"
          @click="getWeather()"
        >
          Get Weather
        </button>
      </div>
      <h2 class="subtitle">
        Result Area:
      </h2>
      <div>
        {{ weather }}
      </div>
    </div>
  </div>
</template>

<script>
import Logo from '~/components/Logo.vue'

const OWM_API_KEY = process.env.OWM_API_KEY;
const UNITS = process.env.UNITS;

export default {    
  components: {
    Logo
  },
  
  data() {
    return {
      city: null,
      weather: null,
      err: null
    }
  },
  
  methods: {
    async getWeather() {
      console.log("UNITS:", UNITS);
      console.log("OWM_API_KEY:", OWM_API_KEY);

      try {
        let url = "http://api.openweathermap.org/data/2.5/weather?" + 
                  "q=" + this.city + 
                  "&units=" + UNITS +
                  "&appid=" + OWM_API_KEY;
        
        let result = await this.$axios.get(url)
        console.log(result)
        
        this.weather = result.data

      } catch (err) {
        console.error(err);
        this.weather = err
      }
    }
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
