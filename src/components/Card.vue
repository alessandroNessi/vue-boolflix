<template>
    <div class="card"  @mouseleave="showImg" @mouseenter="hideImg">
        <img class="cardImage" :src="`https://image.tmdb.org/t/p/w300/${this.filmObject.poster_path}`" :alt="this.filmObject.title">
        <div class="content">
            <h3>Titolo: {{this.filmObject.title}}</h3>
            <div class="d-flex">
                <p>Lingua: {{this.filmObject.original_language}}</p>
                <img class="flagIcon" :src="`https://www.unknown.nu/flags/images/${this.filmObject.original_language}-100`">
            </div>
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
    watch:{
        filmObject: function(value){
            console.log(value);
        }
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
    // @import 'https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta2/css/all.min.css';
    .card{
        position: relative;
        height: 20rem;
        padding: 10px;
        border: 0px solid transparent!important;;
        background-color: $std_bgr!important;
        display: flex;
        flex-direction: row!important;;
        overflow: hidden;
        .d-flex{
            display: flex;
        }
        .flagIcon{
            margin-left: 4px;
            width: 20px;
            height: 15px;
        }
        .cardImage{
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