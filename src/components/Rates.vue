<template>
  <div class="col">
    <h3>Наименование валюты:
      <p class="mt-1">
        <em>{{ title }}</em>
      </p>
    </h3>
    <h1>Курс: {{ course }} euro</h1>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Rates',
  props: {
    title: String,
    shortTitle: String
  },
  data () {
    return {
      rates: {}
    }
  },
  computed: {
    course () {
      if (!this.shortTitle) {
        return '1'
      } else {
        let value = null
        for (const key in this.rates) {
          if (key === this.shortTitle) {
            value = this.rates[key]
          }
        }
        return value
      }
    }
  },
  methods: {
    async findRates () {
      try {
        this.rates = (await axios.get('http://data.fixer.io/api/latest?access_key=7680e5a9853e6328e26067da015dc303')).data.rates
        this.contry = (await axios.get('http://country.io/currency.json')).data
      } catch (error) {
        console.log(error)
      }
    }
  },
  mounted () {
    this.findRates()
  }
}
</script>

<style>

</style>
