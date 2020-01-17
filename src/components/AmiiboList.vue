<template>
  <ul>
      <amiibo-list-item v-for="amiibo in amiibos" :amiibo="amiibo"></amiibo-list-item>
  </ul>
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