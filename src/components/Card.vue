<template>
    <div class="card"  @mouseleave="showImg" @mouseenter="hideImg">
        <img class="cardImage" :src="this.filmObject.poster_path==null?require(`../assets/img/no_image.jpg`):`https://image.tmdb.org/t/p/w300/${this.filmObject.poster_path}`" :alt="this.filmObject.type=='film'? this.filmObject.title : this.filmObject.type">
        <div class="content">
            <h3>Titolo: {{this.filmObject.type=='film'? this.filmObject.title : this.filmObject.name}}</h3>
            <div class="d-flex">
                <p>Lingua: {{this.filmObject.original_language}}</p>
                <img class="flagIcon" :src="`https://www.unknown.nu/flags/images/${this.filmObject.original_language}-100`">
            </div>
            <h4>Titolo originale: {{this.filmObject.type=='film'? this.filmObject.original_title : this.filmObject.original_name}}</h4>
            <p>Voto: {{this.filmObject.vote_average}}<span class="golden"><i v-for="(element, index) in Math.round(this.filmObject.vote_average/2)" :key="index" class="fas fa-star"></i></span><span class="gray"><i v-for="(element, index) in Math.round((10-this.filmObject.vote_average)/2)" :key="index" class="fas fa-star"></i></span></p>
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
            event.target.getElementsByClassName("cardImage")[0].style.display = "none";
        },
        showImg: function(event){
            event.target.getElementsByClassName("cardImage")[0].style.display = "block";
        },
    },
    computed:{
    }
}
</script>

<style lang="scss" scoped>
    @import '../assets/style/common.scss';
    .card{
        position: relative;
        width: 300px!important;
        margin-top: 16px;
        padding: 2px!important;
        height: 430px;
        
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
                margin-bottom: 0.2rem;
            }
            background-color: turquoise;
        }
        .golden{
            color: gold;
        }
        .gray{
            color: slategray;
        }
    }
</style>