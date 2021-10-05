<template>
  <header>
      <input id="searchInput" type="text">
      <button @click="callEmit">submit</button>
  </header>
</template>

<script>
export default {
    name: 'Header',
    data(){
        return{

        }
    },
    methods:{
        callEmit(){
            const emitValue= document.getElementById("searchInput").value;
            if(emitValue!=""){
                this.$emit('emittedSearch',emitValue);
            }
        }
    }
}
</script>

<style scoped lang="scss">
    header{
        height: 13rem;
        background-color: palegreen;
    }
</style>