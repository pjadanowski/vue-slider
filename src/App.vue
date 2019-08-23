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
              'https://picsum.photos/400',
              'https://picsum.photos/id/1000/400',
              'https://picsum.photos/id/1001/400',
              'https://picsum.photos/id/1002/400',
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
