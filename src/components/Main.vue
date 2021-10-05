<template>
  <main>
      <div class="container">{{stringPassed}}
          <div class="row">
              <Card class="p-2  col-xl-4 col-md-6 col-12" v-for="(element, index) in this.filmArray" :key="index" :filmObject="element" />
          </div>
      </div>
  </main>
</template>

<script>
import axios from 'axios';
// import bootstrap from 'bootstrap';
import Card from './Card.vue';
export default {
    name: 'Main',
    components: {
        Card,
    },
    props:{
        stringPassed: String,
    },
    data(){
        return{
            callRoot:"https://api.themoviedb.org/3/search/movie",
            filmArray:[],
        }
    },
    methods:{

    },
    beforeUpdate(){
        axios.get(this.callRoot, {
            params: {
                api_key: "a21aee6674cb415ea0fe118a1c90c893",
                language: "it",
                query: this.stringPassed,
            }   
        }).then((response)=>{
            this.filmArray=response.data.results;
            console.log(this.filmArray);
        });
    }
}
</script>

<style lang="scss" scoped>
    @import '~bootstrap/scss/bootstrap.scss';
    main{
        height: calc(100vh - 13rem);
        background-color: peachpuff;
        overflow: auto;
    }
</style>