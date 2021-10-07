<template>
    <div class="card"  @mouseleave="showImg" @mouseenter="hideImg">
        <img class="cardImage" :src="this.filmObject.poster_path==null?require(`../assets/img/no_image.jpg`):`https://image.tmdb.org/t/p/w300/${this.filmObject.poster_path}`" :alt="this.filmObject.type=='film'? this.filmObject.title : this.filmObject.type">
        <div class="content">
            <p><span class="info__type">Titolo: </span>{{this.filmObject.type=='film'? this.filmObject.title : this.filmObject.name}}</p>
            <p><span class="info__type">Titolo originale: </span> {{this.filmObject.type=='film'? this.filmObject.original_title : this.filmObject.original_name}}</p>
            <p><span class="info__type">Cast: </span>{{this.filmObject.actors}}</p>
            <div class="d-flex">
                <p><span class="info__type">Lingua: </span> {{this.filmObject.original_language}}</p>
                <img class="flagIcon" :src="`https://www.unknown.nu/flags/images/${this.filmObject.original_language}-100`">
            </div>
            <p><span class="info__type">Voto: </span> <span class="golden"><i v-for="(element, index) in Math.round(this.filmObject.vote_average/2)" :key="index" class="fas fa-star"></i></span><span class="gray"><i v-for="(element, index) in Math.round((10-this.filmObject.vote_average)/2)" :key="index" class="fas fa-star"></i></span></p>
            <p><span class="info__type">Overview: </span> {{this.filmObject.overview}}</p>
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
            filmCast:[],
        }
    },
    watch:{
        // filmObject: function(value){
        //     console.log(value);
        // }
    },
    methods:{
        hideImg: function(event){
            event.target.getElementsByClassName("cardImage")[0].style.display = "none";
        },
        showImg: function(event){
            event.target.getElementsByClassName("cardImage")[0].style.display = "block";
        },
        // actors(){
        //     const actors=this.filmObject.actors;
        //     console.log(this.filmObject.actors);
        //     console.log(actors);
        //     let returningString="";
            // , index=0;
            // while(index<5 && index<array.length){
            //     returningString+=array[index]+" ";
                    // index++;
            // }
        //     return returningString;
        // }
    },
    created(){
        this.filmCast=(this.filmObject.actors);
        console.log(this.filmCast);
        console.log(this.filmObject);
        // let temp=[];
        // temp=this.filmCast.actors.forEach(element => {
        //     temp.push(element);        
        // });
        // console.log(this.filmCast.actors);
        // console.log(temp);
            // let returningString="", index=0;
            // console.log(this.filmObject.actors);
            // while(index<5){
            //     returningString+=this.filmObject.actors[index]+" ";
            //     index++;
            // }
            // return returningString;
    },
}
</script>

<style lang="scss" scoped>
    @import '../assets/style/common.scss';
    .card{
        position: relative;
        width: 300px!important;
        margin: 10px 5px 10px 5px;
        padding: 2px!important;
        height: 430px;
        border: 0px solid transparent!important;;
        background-color: $std_bgr!important;
        display: flex;
        flex-direction: row!important;
        color: $text_color;
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