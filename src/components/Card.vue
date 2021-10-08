<template>
    <div class="card_container">
        <div class="card"  @mouseleave="showImg" @mouseenter="hideImg">
            <img class="cardImage" :src="this.filmObject.poster_path==null?require(`../assets/img/no_image.jpg`):`https://image.tmdb.org/t/p/w300/${this.filmObject.poster_path}`" :alt="this.filmObject.type=='film'? this.filmObject.title : this.filmObject.type">
            <div class="content">
                <p><span class="info__type">Titolo: </span>{{this.filmObject.type=='film'? this.filmObject.title : this.filmObject.name}}</p>
                <p><span class="info__type">Titolo originale: </span> {{this.filmObject.type=='film'? this.filmObject.original_title : this.filmObject.original_name}}</p>
                <p><span class="info__type">Cast: </span>{{this.filmCast}}</p>
                <p><span class="info__type">Genere: </span>{{this.filmObject.genre_names}}</p>
                <div class="d-flex">
                    <p><span class="info__type">Lingua: </span> {{this.filmObject.original_language}}</p>
                    <img class="flagIcon" :src="`https://www.unknown.nu/flags/images/${this.filmObject.original_language}-100`">
                </div>
                <p><span class="info__type">Voto: </span> <span class="golden"><i v-for="(element, index) in Math.round(this.filmObject.vote_average/2)" :key="index" class="fas fa-star"></i></span><span class="gray"><i v-for="(element, index) in Math.round((10-this.filmObject.vote_average)/2)" :key="index" class="fas fa-star"></i></span></p>
                <a v-if="this.filmObject.trailerKey" :href="`https://www.youtube.com/watch?v=${this.filmObject.trailerKey}`" class="trailer">watch trailer</a>
                <!-- <p><span class="info__type">Overview: </span> {{this.filmObject.overview}}</p> -->
            </div>
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
    data(){
        return{
            filmCast:"",
        }
    },
    methods:{
        hideImg: function(event){
            event.target.getElementsByClassName("cardImage")[0].style.display = "none";
        },
        showImg: function(event){
            event.target.getElementsByClassName("cardImage")[0].style.display = "block";
        },
    },
    created(){
        let cast=this.filmObject.actors, index=0;
        console.log(this.filmObject);
        if(cast!=undefined){
            while(index<5 && index<cast.length){   
                this.filmCast+=cast[index]+" ";
                index++;
            }
        }
    },
}
</script>

<style lang="scss" scoped>
    @import '../assets/style/common.scss';
    .card{
        &_container{
            transform: rotate(90deg) translateY(-430px);
            transform-origin: left top;
            height: 304px;
        }
        position: relative;
        width: 300px!important;
        padding: 2px!important;
        height: 430px;
        border: 0px solid transparent!important;;
        background-color: $std_bgr!important;
        display: flex;
        flex-direction: row!important;
        color: $text_color;
        .trailer{
            padding: 10px;
            background-color: grey;
            border: 1px solid black;
            border-radius: 5px;
        }
        .info__type{
            font-weight: 600;
        }
        .d-flex{
            display: flex;
        }
        .flagIcon{
            margin-left: 4px;
            width: 20px;
            height: 15px;
        }
        .cardImage{
            width: calc(100% - 4px);
            height: calc(100% - 4px);
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
        }
        .content{
            width: 100%;
            padding: 1rem;
            height: 100%;
            *{
                margin-bottom: 0.5rem;
            }
            background-color: $black_bgr;
            overflow: auto;
        }
        .golden{
            color: gold;
        }
        .gray{
            color: slategray;
        }
    }
</style>