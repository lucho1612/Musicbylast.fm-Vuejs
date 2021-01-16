<template>
  <div id="app">
    <!-- <holaMundo></holaMundo> -->
    <img src="./assets/logo.png">
    <h1>{{ title }}</h1>
    <select v-model="selected">
      <option v-for="country in countries" v-bind:value="country.value">
        {{ country.name }}
      </option>
    </select>
    <spinner v-show="loading"></spinner>
    <ul>
      <artist v-for="artist in artists" :artist="artist" :key="artist.mbid" ></artist>
    </ul>
   
  </div>
</template>

<script>
import  holaMundo  from './holaMundo';
import  getArtists from './api/index.js'
import  Artist  from './components/Artist'
// import  Spinner  from './components/Spinner'
import Spinner from './components/Spinner.vue';

export default {
  name: 'app',
  data () {
    return {
      title: 'TopArtists by Last.fm for Luis Ibarguen ',
      artists: [],
      loading: true,
      selected: 'colombia',
      countries: [
        {name:'Colombia', value: 'colombia'},
        {name:'Argentina', value: 'argentina'},
        {name:'España', value: 'spain'},
      ],
    }
  },
  methods: {
    refreshArtist(){
      const self = this;
      this.loading = true
      this.artists = []
      getArtists(this.selected)
        .then(function (artists) {
          self.loading = false
          self.artists = artists
        })
    }
  },
  mounted() {
   this.refreshArtist()
  },
  watch: {
    selected() {
      this.refreshArtist()
    }
  },
  components: {
    holaMundo,
    Artist,
    Spinner,

  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
