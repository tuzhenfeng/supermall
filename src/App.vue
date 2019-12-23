<template>
  <div id="app">
    <router-view></router-view>
    <tabbar></tabbar>
  </div>
</template>

<script>
import tabbar from './components/tabbar/maintabbar'
export default {
  components:{
    tabbar
  },
  name: 'app'
}
</script>

<style>
@import 'assets/css/base.css'
</style>
