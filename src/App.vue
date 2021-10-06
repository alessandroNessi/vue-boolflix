<template>
  <div id="app">
    <Header @emittedSearch="callAxios"/>
    <Main :filmsGenres="this.filmsGenres" :seriesGenres="this.seriesGenres" :seriesArray="this.seriesArray" :filmsArray="this.filmsArray"/>
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
      callGenres:"https://api.themoviedb.org/3/genre",
      filmsArray:[],
      seriesArray:[],
      filmsGenres:[],
      seriesGenres:[],
    }
  },
  methods:{
    callAxios(str){
      // let temp=[];
      axios.get(this.callMovie, {
            params: {
                api_key: "a21aee6674cb415ea0fe118a1c90c893",
                language: "it",
                query: str,
            }   
        }).then((response)=>{
            response.data.results.map((element)=>{element.type="film"; element.visibility=true});
            this.filmsArray=response.data.results;
            axios.get(this.callSeries, {
              params: {
                  api_key: "a21aee6674cb415ea0fe118a1c90c893",
                  language: "it",
                  query: str,
              }   
              }).then((response)=>{
                  response.data.results.map((element)=>{element.type="serie"; element.visibility=true});
                  // temp.push(...response.data.results);
                  this.seriesArray=response.data.results;
                  // this.filmsArray=temp;
                  // console.log(temp);
                  console.log(response.data.results);
              });
            // console.log(this.filmsArray);
        });
    },
  },
  created(){
    //get movie genres
    axios.get(this.callGenres+"/movie/list", {
      params: {
        api_key: "a21aee6674cb415ea0fe118a1c90c893",
        language: "it-IT",
      }
    }).then((response)=>{
      this.filmsGenres=response.data.genres;
    });
    //get serie genres
    axios.get(this.callGenres+"/tv/list", {
      params: {
        api_key: "a21aee6674cb415ea0fe118a1c90c893",
        language: "it-IT",
      }
    }).then((response)=>{
      this.seriesGenres=response.data.genres;
      console.log(this.seriesGenres);
    });
  }
}
</script>

<style lang="scss">
  @import './assets/style/common.scss'
</style>
