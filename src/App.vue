<template>
    <TextInterface />
</template>

<script>
import TextInterface from './components/TextInterface.vue'

export default {
  name: 'App',
  components: {
    TextInterface
  },
  data: function () {
    return {
      image: '..assets/background.jpg',
    }
  }
}
</script>

<style>
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    z-index: -1;

}

html, body {
  margin: 0;
  padding: 0;
  position: absolute;
  height: 100vh;
  width: 100vw
}
</style>
