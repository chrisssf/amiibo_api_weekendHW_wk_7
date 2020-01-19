<template>
    <div v-if="amiibo.name">
        <h3>{{amiibo.name}}</h3>
        <p>Game: {{amiibo.gameSeries}}</p>
        <p>Series: {{ amiibo.amiiboSeries }}</p>
        <img :src="amiibo.image" alt="">
    </div>
</template>

<script>
export default {
    name: 'amiibo-details',
    props: ['amiibo']

}
</script>

<style scoped>

img {
    width: 150px;
}

</style>