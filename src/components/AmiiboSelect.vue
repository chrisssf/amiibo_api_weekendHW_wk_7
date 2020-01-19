<template>
    <div>
        <form>
            <div v-for="(filterOption, index) in filterOptions" :key="index">
                <input v-model="filterValue" v-on:click="handleClick(filterOption)" type="radio" name="filter" :value="filterOption">{{filterOption}}
            </div>
                                <!-- :checked="checkFigure(filterOption)" -->

                <!-- <input v-model="filterValue" v-on:click="handleClick('all')" type="radio" name="filter" value="all">All -->
            
            <!-- <input v-model="filterValue" v-on:click="handleClick()" value="Figure" checked="checked" type="radio" name="filter" >Figure
            <input v-model="filterValue" v-on:click="handleClick()" value="Card" type="radio" name="filter" >Card
            <input v-model="filterValue" v-on:click="handleClick()" value="Yarn" type="radio" name="filter" >Yarn -->
        </form>
        <select v-on:change="handleChange" v-model="selectedGameSeries">
            <option v-for="(game, index) in gameSeriess" :value="game" :key="index">{{game}}</option>
        </select>
    </div>
</template>

<script>
import { eventBus } from '../main'
export default {
    name: "select-amiibo",
    data() {
        return {
            'selectedGameSeries': null,
            'filterValue': "Figure"
        }
    },
    props: ['gameSeriess', 'filterOptions'],
    methods: {
        handleChange(){
            eventBus.$emit('selected-game-series', this.selectedGameSeries)
        },
        // handleClick(filterOption){
        //     // this.filterValue = filterOption
        //     eventBus.$emit('filtered-value', filterOption)
        // },
        handleClick(filterOption){
            // this.filterValue = filterOption
            eventBus.$emit('filtered-value', filterOption)
        },
        // checkFigure(filterOption){
        //     if (filterOption === 'Figure') {
        //         // this.filterValue = filterOption
        //         // eventBus.$emit('filtered-value', filterOption)      
        //         return "checked"
        //     }
        // }
        
    },
    updated() {
        eventBus.$emit('filtered-value', this.filterValue)
    }
    // mounted() {
    //     eventBus.$emit('filtered-value', this.filterValue)
    // }
}
</script>

<style>

</style>