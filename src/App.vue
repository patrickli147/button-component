<template>
  <div class="app">
    hello
    <Home></Home>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'; //编写类样式组件
import Home from '@/Home.vue';

//装饰器 把类当做组件（component）使用
@Component({
  components: {
    Home
  }
})
export default class App extends Vue {} // export default导出以供其他组件使用
</script>

<style lang="stylus">
#app
  font-family Avenir, Helvetica, Arial, sans-serif
  -webkit-font-smoothing antialiased
  -moz-osx-font-smoothing grayscale
  text-align center
  color #2c3e50
  margin-top 60px
</style>
