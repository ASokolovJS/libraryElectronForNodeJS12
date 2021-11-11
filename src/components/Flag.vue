<template>
  <div class="col-6 text-center">
    <img class="img-thumbnail"
      :src="'https://flagcdn.com/w160/'+ flags +'.png'"
      width="164">
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Flag',
  props: {
    shortTitle: String
  },
  data () {
    return {
      contry: {},
      shortTitles: this.shortTitle
    }
  },
  computed: {
    flags () {
      if (!this.shortTitle) {
        return 'ru'
      } else {
        return (Object.keys(this.contry).find(key => this.contry[key] === this.shortTitle)).toLowerCase()
      }
    }
  },
  methods: {
    async findFlag () {
      try {
        this.contry = (await axios.get('http://country.io/currency.json')).data
      } catch (error) {
        console.log(error)
      }
    }
  },
  mounted () {
    this.findFlag()
  }
}

</script>
