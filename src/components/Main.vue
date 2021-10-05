<template>
  <main>
      <div class="container">
          <div class="row">
              <Card class="col-xl-4 col-md-6 col-12" v-for="(element, index) in this.filmArray" :key="index" :filmObject="element" />
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
        filmArray: Array,
    },
    data(){
        return{

        }
    },
    methods:{

    },
    beforeUpdate(){

    }
}
</script>

<style lang="scss" scoped>
    @import '../assets/style/common.scss';
    @import '~bootstrap/scss/bootstrap.scss';
    main{
        height: calc(100vh - 13rem);
        background-color: peachpuff;
        overflow: auto;
    }
</style>