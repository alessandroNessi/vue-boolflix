<template>
  <main>
      <div class="container">{{stringPassed}}</div>
  </main>
</template>

<script>
import axios from 'axios';
export default {
    name: 'Main',
    props:{
        stringPassed: String,
    },
    data(){
        return{
            callRoot:"https://api.themoviedb.org/3/search/movie",

        }
    },
    methods:{

    },
    updated(){
        axios.get(this.callRoot, {
            params: {
                api_key: "a21aee6674cb415ea0fe118a1c90c893",
                language: "it",
                query: this.stringPassed,
            }   
        }).then(function (response) {
            console.log(response.data.results);
        });
    }
}
</script>

<style lang="scss" scoped>
    main{
        height: calc(100vh - 13rem);
        background-color: peachpuff;
    }
</style>