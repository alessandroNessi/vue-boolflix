<template>
    <div class="card">
        <img :src="`https://image.tmdb.org/t/p/w300/${this.filmObject.poster_path}`" :alt="this.filmObject.title">
        <div class="content">
            <h3>Titolo: {{this.filmObject.title}}</h3>
            <p>Lingua: {{this.filmObject.original_language}}</p>
            <h4>Titolo originale: {{this.filmObject.original_title}}</h4>
            <p>Voto: {{this.filmObject.vote_average}}</p>
        </div>
    </div>
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
    @import '../assets/style/common.scss';
    .card{
        height: 10rem;
        padding: 10px;
        border: 0px solid transparent!important;;
        background-color: $std_bgr!important;
        display: flex;
        flex-direction: row!important;;
        img{
            width: 7rem;
            // height: 100%;
            // display: inline-block;
        }
        .content{
            padding: 1rem;
            flex-grow: 1;
            height: 100%;
            *{
                margin-bottom: 0.2rem;
            }
            background-color: turquoise;
            overflow: auto;
        }
    }
</style>