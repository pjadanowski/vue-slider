<template>
  <div id="app">
<!--    <img alt="Vue logo" src="./assets/logo.png">-->
    <Gallery :images="images"/>
  </div>
</template>

<script>
import Gallery from './components/Gallery.vue'

export default {
  name: 'app',
  data() {
    return {
      images: [
              'https://picsum.photos/600',
              'https://picsum.photos/2600/600',
              'https://picsum.photos/300/2600',
              'https://picsum.photos/1002/600',
      ],
      currentSlide: 0,
      timer: null
    }
  },
  methods: {
    startSlide() {
      this.timer = setInterval(this.next, 3000)
    },
    next() {
      this.currentSlide += 1
    }
  },
  components: {
    Gallery
  },
  mounted() {
    this.startSlide()
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
</style>
