<template>
  <div id="app">
    <Header @emittedSearch="callAxios"/>
    <Main :filmArray="this.filmArray"/>
  </div>
</template>

<script>
import Header from './components/Header.vue';
import Main from './components/Main.vue'
import axios from 'axios';

export default {
  name: 'App',
  components: {
    Header,
    Main,
  },
  data(){
    return{
      stringToGet:'',
      callRoot:"https://api.themoviedb.org/3/search/movie",
      filmArray:[],
    }
  },
  methods:{
    callAxios(str){
      axios.get(this.callRoot, {
            params: {
                api_key: "a21aee6674cb415ea0fe118a1c90c893",
                language: "it",
                query: str,
            }   
        }).then((response)=>{
            this.filmArray=response.data.results;
            console.log(this.filmArray);
        });
    }
  }
}
</script>

<style lang="scss">
  @import './assets/style/common.scss'
</style>
