<template>
  <select v-on:change="handleChange" v-model="selectedGameSeries">
      <option v-for="game in gameSeriess" :value="game">{{game}}</option>
  </select>

</template>

<script>
import { eventBus } from '../main'
export default {
    name: "select-amiibo",
    data() {
        return {
            'selectedGameSeries': null
        }
    },
    props: ['gameSeriess'],
    methods: {
        handleChange(){
            eventBus.$emit('selected-game-series', this.selectedGameSeries)
        }
    }
}
</script>

<style>

</style>