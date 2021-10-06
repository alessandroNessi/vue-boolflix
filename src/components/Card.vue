<template>
    <div class="card"  @mouseleave="showImg" @mouseenter="hideImg">
        <img class="cardImage" :src="`https://image.tmdb.org/t/p/w300/${this.filmObject.poster_path}`" :alt="this.filmObject.title">
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
        index:Number,
    },
    methods:{
        hideImg: function(event){
            console.log(event.target);
            event.target.getElementsByClassName("cardImage")[0].style.display = "none";
            // document.getElementsByClassName("cardImage")[0].style.display = "none";
        },
        showImg: function(event){
            console.log(event.target);
            event.target.getElementsByClassName("cardImage")[0].style.display = "block";
            // document.getElementsByClassName("cardImage")[0].style.display = "none";
        },
    },
}
</script>

<style lang="scss" scoped>
    @import '../assets/style/common.scss';
    .card{
        position: relative;
        height: 20rem;
        padding: 10px;
        border: 0px solid transparent!important;;
        background-color: $std_bgr!important;
        display: flex;
        flex-direction: row!important;;
        overflow: hidden;
        img{
            width: calc(100% - 20px);
            height: calc(100% - 20px);
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            // z-index: -1;
        }
        .content{
            width: 100%;
            padding: 1rem;
            flex-grow: 1;
            height: 100%;
            *{
                margin-bottom: 0.2rem;
            }
            background-color: turquoise;
        }
    }
</style>