<template>
    <div>
        <p>{{amiibo.name}}</p>
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