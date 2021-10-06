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
      callMovie:"https://api.themoviedb.org/3/search/movie",
      callSeries:"https://api.themoviedb.org/3/search/tv",
      filmArray:[],
    }
  },
  methods:{
    callAxios(str){
      let temp=[];
      axios.get(this.callMovie, {
            params: {
                api_key: "a21aee6674cb415ea0fe118a1c90c893",
                language: "it",
                query: str,
            }   
        }).then((response)=>{
            response.data.results.map((element)=>{element.type="film"});
            temp=response.data.results;
            axios.get(this.callSeries, {
              params: {
                  api_key: "a21aee6674cb415ea0fe118a1c90c893",
                  language: "it",
                  query: str,
              }   
              }).then((response)=>{
                  response.data.results.map((element)=>{element.type="serie"});
                  temp.push(...response.data.results);
                  this.filmArray=temp;
                  console.log(temp);
                  console.log(response.data.results);
              });
            // console.log(this.filmArray);
        });
    },
  }
}
</script>

<style lang="scss">
  @import './assets/style/common.scss'
</style>
