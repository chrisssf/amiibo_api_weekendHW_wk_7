<template>
  <div id="app">
    <h1>AMIIBO</h1>
    <amiibo-list :amiibos="amiibos"></amiibo-list>
  </div>
</template>

<script>
import AmiiboList from './components/AmiiboList.vue'
import AmiiboDetails from './components/AmiiboDetails.vue'

export default {
  name: 'app',
  data() {
    return {
      amiibos: []
    }

  },
  components: {
    "amiibo-list": AmiiboList
  },
  mounted() {
    fetch("https://www.amiiboapi.com/api/amiibo/")
    .then(amiiboData => amiiboData.json())
    .then(amiibos => this.amiibos = amiibos.amiibo)
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
