<template>
  <div id="app">
    <Main msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import Main from './components/Main.vue'
export default {
  name: 'App',
  components: {
    Main
  }
}
</script>
<style lang="sass">
@import './styles/_global.sass';
</style>