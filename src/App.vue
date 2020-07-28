<template>
  <div id="app">
    <scroll-view>

    </scroll-view>
  </div>
</template>

<script>
import ScrollView from './components/ScrollView.vue'

export default {
  name: 'App',
  components: {
    ScrollView
  }
}
</script>
<style lang="stylus">
body
  margin 0
*
  box-sizing border-box
</style>
<style lang="stylus" scoped>
#app 
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  height 100vh;

</style>
