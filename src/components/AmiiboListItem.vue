<template>
  <li v-on:click="handleClick"><img :src="amiibo.image" alt=""></li>
</template>

<script>

import {eventBus} from '../main'

export default {
    name: 'amiibo-list-item',
    props: ['amiibo'],
    methods: {
        handleClick() {
            eventBus.$emit('selected-amiibo', this.amiibo)
        }

    }

}
</script>

<style scoped>

li {
    list-style: none;
    display: inline;
}

img {
    width: 50px;
}

</style>