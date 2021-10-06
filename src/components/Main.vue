<template>
  <main>
      <div class="container">
          <!-- films -->
          <div class="row_title">
            <h2>FILMS</h2>
            <!-- v-model="this.filmsel" -->
            <select  @change="Filtering(document.getElementById('filmselected').value,this.filmsArray)" name="filmselect" id="filmselect">
                <option value="">tutti i generi</option>
                <option v-for="(element,index) in this.filmsGenres" :key="index" :value="element.id">{{element.name}}</option>
            </select>
          </div>
          <div class="row">
              <Card class="card__film col-xxl-2 col-xl-3 col-lg-4 col-md-6 col-12" v-for="(element, index) in this.filmsArray" :key="index" :class="{'d-none':!element.visibility}" :filmObject="element" />
          </div>

        <!-- series -->
          <div class="row_title">
            <h2>SERIE</h2>
            <select name="serieselect" id="serieselect">
                <option value="">tutti i generi</option>
                <option v-for="(element,index) in this.seriesGenres" :key="index" :value="element.id">{{element.name}}</option>
            </select>
          </div>
          <div class="row">
              <Card class="card__serie col-xxl-2 col-xl-3 col-lg-4 col-md-6 col-12" v-for="(element, index) in this.seriesArray" :key="index" :filmObject="element" />
          </div>
      </div>
  </main>
</template>

<script>
import Card from './Card.vue';
export default {
    name: 'Main',
    components: {
        Card,
    },
    props:{
        filmsArray: Array,
        seriesArray: Array,
        seriesGenres: Array,
        filmsGenres: Array,
    },
    data(){
        return{
            filmsel:"",
        }
    },
    methods:{
        Filtering(genre, array){
            let type=parseInt(genre);
            console.log(this.filmsel);
            array.forEach((element) => {
                if(element.genre_ids.includes(type)){
                    element.visibility=true;
                }else{
                    element.visibility=false;
                }
            });
        }
    }
}
</script>

<style lang="scss" scoped>
    @import '../assets/style/common.scss';
    @import '~bootstrap/scss/bootstrap.scss';
    main{
        height: calc(100vh - $header_height);
        background-color: $gray_bgr;
        overflow: auto;
        h2{
            color: $text_color;
            text-align: center;
            padding: 10px;
            margin-bottom: 0;
        }
        .row_title{
            display: flex;
            justify-content: center;
            align-items: center;
            select{
                height: 2rem;
            }
        }
    }
    .row{
        justify-content: center;
        border: 1px solid #aaa;
        // ::-webkit-scrollbar {
        //     display: none;
        //     width: 0;
        // }
        // -ms-overflow-style: none;
        // scrollbar-width: 0;
        height: 50rem;
        overflow: auto;
        
    }
</style>