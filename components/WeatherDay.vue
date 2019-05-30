<template lang="pug" v-if="forecast && forecast.main">
  .container.weather-box(v-if="forecast && forecast.main")

    img.weather-box-icon(src="~/assets/hot-weather.png" v-if="convertKelvinToCelcius(forecast.main.temp) > 25")
    img.weather-box-icon(v-else src='~/assets/cold-weather.png')

    span.weather-box-temp {{ convertKelvinToCelcius(forecast.main.temp) }}°C
    span.weather-box-pressure Presion {{ forecast.main.pressure }}
    span.weather-box-humidity Humedad {{ forecast.main.humidity }}

    div.weather-box-ranges
      span.weather-box-ranges-text Minima {{ convertKelvinToCelcius(forecast.main.temp_min) }}°C
      span.weather-box-ranges-text Maxima {{ convertKelvinToCelcius(forecast.main.temp_max) }}°C

    span.weather-box-last-update Ultima actualizacion: {{ time }}
</template>

<script>
import moment from 'moment'

export default {
  props: {
    forecast: {
      type: Object,
      default: () => ({})
    }
  },
  data: () => ({ time: moment().format('LT') }),
  methods: {
    convertKelvinToCelcius(kelvinTemperature) {
      return Math.floor(kelvinTemperature - 273.15)
    }
  }
}
</script>

<style lang="scss">
.weather-box {
  display: flex;
  flex-direction: column;
  font-family: 'Montserrat', sans-serif;
  align-items: center;
  justify-content: center;
  height: calc(90vh - 112px);

  &-icon {
    width: 100px;
  }

  &-temp {
    font-size: 48px;
  }

  &-ranges {
    display: flex;

    &-text {
      font-weight: 500;
      font-size: 14px;
      margin: 0px 4px 0px 4px;
    }
  }

  &-pressure,
  &-humidity {
    font-size: 15px;
  }

  &-last-update {
    font-size: 12px;
    font-style: italic;
  }
}
</style>
