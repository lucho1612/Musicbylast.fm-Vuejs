<template>
    <div>
        <li>
            <h2>
                <a :href="artist.url" target="blank"> {{artist.name }} </a>
            </h2>
            <img :src="artist.image[3]['#text']">
        </li>
    </div>
</template>

<script>
    export default {
        name: 'artist',
        props:['artist']
    }
</script>

<style scoped>
    li{
        display: block;
        margin: 10px 0;
    }
</style>