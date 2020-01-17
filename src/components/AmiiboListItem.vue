<template>
  <li><img :src="amiibo.image" alt=""></li>
</template>

<script>
export default {
    name: 'amiibo-list-item',
    props: ['amiibo']

}
</script>

<style>

li {
    list-style: none;
    display: inline;
}

img {
    width: 50px;
}

</style>