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
      callMovieActors:"https://api.themoviedb.org/3/movie/",
      callSeriesActors:"https://api.themoviedb.org/3/tv/",
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
      //svuoto i form dei film/serie
      for(let i=0; i<document.getElementsByClassName("row").length;i++){
        document.getElementsByClassName("row")[i].innerHTML="";
      }
      // chiamata film
      const researchParams={api_key: "a21aee6674cb415ea0fe118a1c90c893",language: "it",query: str,};
      const actorsParams={api_key: "a21aee6674cb415ea0fe118a1c90c893",language: "it-IT",};
      axios.get(this.callMovie, {
            params: researchParams
        }).then((response)=>{
            // chiamata attori
            response.data.results.forEach((element) => {
              axios.get(this.callMovieActors+element.id+"/credits", {
                params:actorsParams
              }).then((responseactors)=>{
                let actors=[];
                responseactors.data.cast.forEach(actor=>{actors.push(actor.name);});
                element.actors=actors;
                element.visibility=true;
                element.type="film";
                element.genre_names="";
                element.genre_ids.forEach(element2=>{
                  this.filmsGenres.forEach(element3=>{
                    if(element3.id==element2){
                      element.genre_names+=element3.name+" ";
                    }
                  });
                });
                axios.get("https://api.themoviedb.org/3/movie/"+element.id+"/videos?api_key=a21aee6674cb415ea0fe118a1c90c893&language=it-IT",)
                .then((responseTrailer)=>{
                  if(responseTrailer.data.results[0]!=undefined){
                    element.trailerKey=responseTrailer.data.results[0].key;
                  }else{
                    element.trailerKey=false;
                  }
                  this.filmsArray.push(element);
                });
              });
            });
            //fine chiamata attori
            axios.get(this.callSeries, {
              params: researchParams
              }).then((response)=>{
                // chiamata attori
                response.data.results.forEach((element) => {
                  axios.get(this.callSeriesActors+element.id+"/credits", {
                    params:actorsParams
                  }).then((responseactors)=>{
                    let actors=[];
                    responseactors.data.cast.forEach(actor=>{actors.push(actor.name);});
                    element.actors=actors;
                    element.visibility=true;
                    element.type="serie";
                    element.genre_names="";
                    element.genre_ids.forEach(element2=>{
                      this.seriesGenres.forEach(element3=>{
                        if(element3.id==element2){
                          element.genre_names+=element3.name+" ";
                        }
                      });
                    });
                    this.seriesArray.push(element);
                  });
                });
                //fine chiamata attori
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
    });
  }
}
</script>

<style lang="scss">
  @import './assets/style/common.scss'
</style>
