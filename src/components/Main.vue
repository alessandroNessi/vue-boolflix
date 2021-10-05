<template>
  <main>
      <div class="container">{{stringPassed}}</div>
  </main>
</template>

<script>
export default {
    name: 'Main',
    props:{
        stringPassed: String,
    },
    data(){
        return{

        }
    },
    methods:{

    },
    computed:{

    }
}
</script>

<style lang="scss" scoped>
    main{
        height: calc(100vh - 13rem);
        background-color: peachpuff;
    }
</style>