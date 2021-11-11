<template>
  <select class="form-select form-select-lg" v-model="select" @change="sendTitle">
    <option v-for="items in title" :key="items" :value=items>{{items}}</option>
  </select>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Selector',
  data () {
    return {
      sinbol: {},
      title: [],
      select: '',
      shortTitle: ''
    }
  },
  methods: {
    async findTitle () {
      try {
        this.sinbol = (await axios.get('http://data.fixer.io/api/symbols?access_key=7680e5a9853e6328e26067da015dc303')).data.symbols
        this.title = Object.values(this.sinbol)
        console.log(this.select)
      } catch (error) {
        console.log(error)
      }
    },
    sendTitle () {
      this.shortTitle = Object.keys(this.sinbol).find(key => this.sinbol[key] === this.select)
      this.$emit('sendTitle', {
        select: this.select,
        shortTitle: this.shortTitle
      }
      )
    }
  },
  mounted () {
    this.findTitle()
  }

}
</script>

<style>

</style>
