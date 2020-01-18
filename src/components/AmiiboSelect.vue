<template>
    <div>
        <form>
            <div v-for="filterOption in filterOptions">
                <input v-on:click="handleClick(filterOption)" :checked="checkFigure(filterOption)" type="radio" name="filter" :value="filterOption">{{filterOption}}
            </div>
                <input v-on:click="handleClick('all')" type="radio" name="filter" value="all">All
        </form>
        <select v-on:change="handleChange" v-model="selectedGameSeries">
            <option v-for="game in gameSeriess" :value="game">{{game}}</option>
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
            'filterOption': null
        }
    },
    props: ['gameSeriess', 'filterOptions'],
    methods: {
        handleChange(){
            eventBus.$emit('selected-game-series', this.selectedGameSeries)
        },
        handleClick(filterOption){
            this.filterOption = filterOption
            eventBus.$emit('filtered-value', filterOption)
        },
        checkFigure(filterOption){
            if (filterOption === 'Figure') {
                this.filterOption = filterOption
                eventBus.$emit('filtered-value', filterOption)      
                return "checked"
            }
        }
        
    },
    mounted() {
        // eventBus.$emit('filtered-value', this.filter)
    }
}
</script>

<style>

</style>