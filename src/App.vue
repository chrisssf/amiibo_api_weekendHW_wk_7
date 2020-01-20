<template>
  <div id="app">
    <h1>AMIIBO</h1>
    <amiibo-select :gameSeriess="gameSeriess" :filterOptions="filterOptions"></amiibo-select>
    <amiibo-details :amiibo="selectedAmiibo"></amiibo-details>
    <amiibo-list :amiibos="amiibosToList"></amiibo-list>

  </div>
</template>

<script>
import { eventBus } from './main'
import AmiiboSelect from './components/AmiiboSelect'
import AmiiboList from './components/AmiiboList.vue'
import AmiiboDetails from './components/AmiiboDetails.vue'
import AmiiboSelectVue from './components/AmiiboSelect.vue'

export default {
  name: 'app',
  data() {
    return {
      amiibos: [],
      selectedAmiibo: {},
      gameSeriess: [],
      selectedGameSeries: null,
      amiibosMatchingGameSeries: [],
      filterOptions: [],
      filterValue: null
    }
  },
  computed: {
    amiibosToList: function(){
      let amiibosToList = this.amiibos
      if (this.filterValue === "All"){
          if (this.selectedGameSeries !== "All") {
            amiibosToList = this.amiibos.filter(amiibo => amiibo.gameSeries === this.selectedGameSeries)
          }
        return amiibosToList
      } else {
        const amiibosMatchingType = this.amiibos.filter(amiibo => amiibo.type === this.filterValue)
        if (this.selectedGameSeries !== "All") {
          amiibosToList = amiibosMatchingType.filter(amiibo => amiibo.gameSeries === this.selectedGameSeries)
        } else {
          amiibosToList = amiibosMatchingType
        }
        return amiibosToList
      }
    }
  },
  methods: {
  },
  components: {
    "amiibo-list": AmiiboList,
    "amiibo-details": AmiiboDetails,
    "amiibo-select": AmiiboSelect
  },
  mounted() {
    fetch("https://www.amiiboapi.com/api/amiibo/")
    .then(amiiboData => amiiboData.json())
    .then(amiibos => this.amiibos = amiibos.amiibo)
    .then(amiibos => {
      const amiibosSortedByGameSeries = this.amiibos.map(amiibo => amiibo.gameSeries).sort() 
      
      amiibosSortedByGameSeries.forEach((gameSeries, index, array) => {
        if (array[index] !== array[index + 1]) {
          this.gameSeriess.push(gameSeries)
        }
      })
      this.gameSeriess.unshift("All")
    })
    .then( amiibos => {
      const amiibosSortedByType = this.amiibos.map(amiibo => amiibo.type).sort()

      amiibosSortedByType.forEach((filterOption, index, array) => {
        if (array[index] !== array[index + 1]) {
          this.filterOptions.push(filterOption)
        }
      })
      this.filterOptions.push("All")
    })

    eventBus.$on('selected-amiibo', (amiibo) => {
      this.selectedAmiibo = amiibo
    })

    eventBus.$on('selected-game-series', (gameSeries) => {
      this.selectedGameSeries = gameSeries
      const amiibosMatchingGameSeries = this.amiibos.filter(amiibo => amiibo.gameSeries == gameSeries)
      // console.log(amiiboMatchingGameSeriess);
      this.amiibosMatchingGameSeries = amiibosMatchingGameSeries
      
    })
  
    eventBus.$on('filtered-value', (filterValue) => {
      this.filterValue = filterValue
    })
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
