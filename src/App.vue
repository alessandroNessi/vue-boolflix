// z index player 999, always top

<template>
  <div id="app">
    <div id="videoContainer">
      <div class="midContainer">
        <button @mouseup="closeVideo()">X</button>
        <iframe class="videoPlayer" src="">
        </iframe>
      </div>
    </div>
    <Header @emittedSearch="callAxios"/>
    <Main @trailerUrl="startTrailer" :filmsGenres="this.filmsGenres" :seriesGenres="this.seriesGenres" :seriesArray="this.seriesArray" :filmsArray="this.filmsArray"/>
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
    startTrailer(str){
      document.getElementsByClassName("videoPlayer")[0].src=str;
      document.getElementById("videoContainer").style.display="flex";
    },
    closeVideo(){
      document.getElementById("videoContainer").style.display="none";
      console.log(document.getElementsByClassName("videoPlayer")[0].contentWindow);
      // document.getElementsByClassName("video-stream")[0].pause();
      // document.getElementsByClassName("videoPlayer")[0].contentWindow.postMessage('{"event":"command","func":"' + 'stopVideo' + '","args":""}', '*');
    },
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
  #videoContainer{
    position: absolute;
    background-color: rgba($color: #000000, $alpha: 0.4);
    width: 100vw;
    height: 100vh;
    display: none;
    justify-content: center;
    align-items: center;
    z-index: 999;
    .midContainer{
      position: relative;
      width: 100%;
      height: 100%;
      max-width: 800px;
      max-height: 600px;
      .videoPlayer{
        width: 100%;
        height: 100%;
        
      }
      button{
        position: absolute;
        border-width: 0;
        height: 50px;
        width: 50px;
        background-color: rgba($color: red, $alpha: 0.7);
        color: white;
        border-radius: 50%;
        top: 0;
        right: 0;
      }
    }
  }
  @import './assets/style/common.scss'
</style>
