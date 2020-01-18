<template>
  <div id="app">
    <h1>AMIIBO</h1>
    <amiibo-select :gameSeriess="gameSeriess"></amiibo-select>
    <amiibo-details :amiibo="selectedAmiibo"></amiibo-details>
    <!-- <amiibo-list v-if="return selectedGameSeries ? :amiibos='selectedGameSeries' : :amiibos='amiibos' "></amiibo-list> -->
    <amiibo-list v-if="selectedGameSeries" :amiibos='amiibosMatchingGameSeries'></amiibo-list>
    <!-- <amiibo-list v-if="" :amiibos='amiibos'></amiibo-list> -->


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
      amiibosMatchingGameSeries: []
    }
  },
  methods: {


    // write function to search for amiibo that have coresponding gameSeriess




    // getGameSeriess(){
    //   const amiibosSortedByGameSeries = this.amiibos.map(amiibo => amiibo.gameSeries).sort() 
      
    //   amiibosSortedByGameSeries.forEach((gameSeries, index, array) => {
    //     if (array[index] !== array[index + 1]) {
    //       this.gameSeriess.push(gameSeries)
    //     }
    //   })
    // }
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
    })

    eventBus.$on('selected-amiibo', (amiibo) => {
      this.selectedAmiibo = amiibo
    })

    eventBus.$on('selected-game-series', (gameSeries) => {
      this.selectedGameSeries = gameSeries
      const amiibosMatchingGameSeries = this.amiibos.filter(amiibo => amiibo.gameSeries == gameSeries)
      // console.log(amiiboMatchingGameSeriess);
      this.amiibosMatchingGameSeries = amiibosMatchingGameSeries
      console.log(gameSeries);
      
      
    })
    

    // // const sortedAmiibos = [...this.amiibos] //may not need to do this if map creates new array
    // const amiibosSortedByGameSeries = this.amiibos.map(amiibo => amiibo.gameSeries).sort() 
    // // loop over and check if index === to index + 1
    // console.log(amiibosSortedByGameSeries);
    
    // amiibosSortedByGameSeries.forEach((gameSeries, index, array) => {
    //   if (array[index] !== array[index + 1]) {
    //     this.gameSeriess.push(gameSeries)
    //   }
    // })
      // if no, add index
      // might need to check amiibo.namesss
    

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
