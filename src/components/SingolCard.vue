<template>
<div class="text-center">

    <img :src="coverPath" alt="">

   

    <h3> <strong>Titolo: {{titolo}}</strong></h3>
    <h4>({{titoloOriginale}})</h4>
    <img class="w-25" v-bind:src="require ( '@/assets/'+ lingua)" alt="">
    <h5>Voto: {{voto}} </h5>
    <h5>Sigla Paese: {{paese}} </h5>

    
        
</div>

 
</template>

<script>
export default {
    name: "SingolCard",

    props:{
        titolo: {String},
        titoloOriginale: { String},
        paese: {String},
        lingua: {Image,
                default:() => "mondo.png"},
        voto: {Number},
        cover: {String}
    }, 

    computed:{
        coverPath() {
            const linkRoot = "https://image.tmdb.org/t/p/";

            const size = "w342";

            if(!this.cover){
                return require("@/assets/noimg.png");
            }

            return linkRoot + size + this.cover ;


        },
    },


}
</script>