<template>
  <div class="container mt-3">
    <div class="card">
      <h3 class="mb-3 text-center">Добро пожаловать в валютный справочник</h3>
      <div class="form-control">
        <Selector @sendTitle="onSend"/>
        <div class="card mt-3">
          <div class="row">
            <Flag v-bind:shortTitle='shortTitle' />
            <Rates :title= title :shortTitle= shortTitle />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Flag from './Flag.vue'
import Selector from './Selector.vue'
import Rates from './Rates.vue'

export default {
  name: 'MainComponent',
  data () {
    return {
      title: '',
      shortTitle: ''
    }
  },
  components: {
    Flag,
    Selector,
    Rates
  },
  methods: {
    onSend (data) {
      this.title = data.select
      this.shortTitle = data.shortTitle
    }
  }
}
</script>

<style scoped>

</style>
