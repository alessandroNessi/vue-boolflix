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
      // https://api.themoviedb.org/3/movie/{movie_id}/credits?api_key=<<api_key>>&language=en-US
      callMovieActors:"https://api.themoviedb.org/3/movie/",
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
      // chiamata film
      const researchParams={api_key: "a21aee6674cb415ea0fe118a1c90c893",language: "it",query: str,};
      const actorsParams={api_key: "a21aee6674cb415ea0fe118a1c90c893",language: "it-IT",};
      axios.get(this.callMovie, {
            params: researchParams
        }).then((response)=>{
            // chiamata attori
            response.data.results.forEach(element => {
              axios.get(this.callMovieActors+element.id+"/credits", {
                params:actorsParams
              }).then((response)=>{
                let actors=[];
                response.data.cast.forEach(actor=>{actors.push(actor.name);});
                element.actors=actors;
              });
            });
            //fine chiamata attori
            response.data.results.map((element)=>{element.type="film"; element.visibility=true});
            this.filmsArray=response.data.results;
            // chiamata serie
            axios.get(this.callSeries, {
              params: researchParams
              }).then((response)=>{
                  response.data.results.map((element)=>{element.type="serie"; element.visibility=true});
                  this.seriesArray=response.data.results;
                  // console.log(response.data.results);
              });
        });
        // fine chiamata film
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
      // console.log(this.seriesGenres);
    });
  }
}
</script>

<style lang="scss">
  @import './assets/style/common.scss'
</style>
