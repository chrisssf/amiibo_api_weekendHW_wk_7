<template>
    <div>
        <ul>
            <amiibo-list-item v-for="amiibo in amiibos" :amiibo="amiibo"></amiibo-list-item>
        </ul>
        <h4 v-if="amiibos.length === 0">Nothing Matches Your Search</h4>
    </div>
</template>

<script>
import AmiiboListItem from './AmiiboListItem.vue'

export default {
    name: 'amiibo-list',
    props: ['amiibos'],
    components: {
        'amiibo-list-item': AmiiboListItem
    }

}
</script>

<style>

</style>