<template lang="pug">
div
  Header
  h2.title Clima en Monterrey, Nuevo Leon
  WeatherDay(:forecast="forecast")
  Footer
</template>

<script>
import { Header, Footer, WeatherDay } from '~/components'

const weatherUrl = 'https://api.openweathermap.org/data/2.5/weather'
const appId = 'e5daf32ba2f76fb213967a894fb35497'
const MONTERREY_CITY_ID = '3995465'

export default {
  components: {
    Header,
    Footer,
    WeatherDay
  },
  data: () => ({ forecast: {} }),
  async mounted() {
    await this.getForecastFromApi(MONTERREY_CITY_ID)
  },
  methods: {
    async getForecastFromApi(cityId) {
      const forecast = await this.$axios.get(
        `${weatherUrl}?id=${cityId}&appId=${appId}`
      )
      this.forecast = forecast.data
    }
  }
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css?family=Montserrat:400,500,600,700&display=swap');
.title {
  text-align: center;
  font-family: 'Montserrat', sans-serif;
  font-size: 24px;
  height: 10vh;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
