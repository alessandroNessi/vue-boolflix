<template>
    <div class="card">{{this.filmObject.title}}</div>
</template>

<script>
export default {
    name: 'Card',
    props:{
        filmObject:Object,
    }
}
</script>

<style lang="scss" scoped>
    // .card{
        // height: 10rem;
        // margin: 10px;
    // }
</style>