<template>
    <div class="container">
        <div class="content">
            <p>Filter by Amiibo Type</p>
            <li v-for="(filterOption, index) in filterOptions" :key="index">
                <input v-model="filterValue" v-on:click="handleClick(filterOption)" type="radio" name="filter" :value="filterOption">{{filterOption}}
            </li>
            <p>Filter by Game Series</p>
            <select v-on:change="handleChange" v-model="selectedGameSeries">
                <option v-for="(game, index) in gameSeriess" :value="game" :key="index">{{game}}</option>
            </select>
        </div>
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
        handleClick(filterOption){
            // this.filterValue = filterOption
            eventBus.$emit('filtered-value', filterOption)
        }
    },
    beforeUpdate(){
        console.log("beforeUpdate");
    },
    updated() {
        eventBus.$emit('filtered-value', this.filterValue)
        console.log("updated");
        
    },
    mounted() {
        // eventBus.$emit('filtered-value', this.filterValue)
        console.log("mounted");
        
    }
}
</script>

<style scoped>

.container {
    display: flex;
    justify-content: center;
}

.content {
    border: 2px solid black;
    max-width: 500px;
    padding: 0px 30px 30px 30px;
}

li {
    display: inline;
    list-style: none;
    margin-right: 50px; 
}
</style>