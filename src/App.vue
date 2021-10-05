<template>
  <div id="app">
    <Header @emittedSearch="passValueToVar"/>
    <Main :stringPassed="this.stringToGet"/>
  </div>
</template>

<script>
import Header from './components/Header.vue';
import Main from './components/Main.vue'

export default {
  name: 'App',
  components: {
    Header,
    Main,
  },
  data(){
    return{
      stringToGet:'',
    }
  },
  methods:{
    passValueToVar(str){
      this.stringToGet=str;
    }
  }
}
</script>

<style lang="scss">
  @import './assets/style/common.scss'
</style>
