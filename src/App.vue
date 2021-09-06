<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <div id="wrap">
      <HelloWorld id="zoom" msg="Welcome to Your Vue.js App"/>
    </div>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import zoomable from 'd3-zoomable'

export default {
  name: 'App',
  components: {
    HelloWorld
  },
  data () {
    return {
      zoom: null
    }
  },
  mounted () {
    // ref로 하면 내부 함수에서 this를 vue 객체로 잡아서 에러남
    // https://vasturiano.github.io/d3-zoomable
    // https://vasturiano.github.io/d3-zoomable/example/html/
    const wrap = document.querySelector('#wrap')
    const zoom = document.querySelector('#zoom')
    const minZoom = 0.5
    const maxZoom = 2
    this.zoom = zoomable()(wrap).htmlEl(zoom).scaleExtent([minZoom, maxZoom])
    setTimeout(() => {
      console.log(innerHeight, wrap.offsetTop)
      const wrapStyle = wrap.style
      wrapStyle.width = `${innerWidth - 4}px`
      wrapStyle.height = `${innerHeight - wrap.offsetTop + 4}px`
    }, 1000)
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
#wrap {
  overflow: auto;
}
#zoom {
  transform-origin: top left;
}
</style>
