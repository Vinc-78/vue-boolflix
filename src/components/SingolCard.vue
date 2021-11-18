<template>
<div class="text-center">

   
    <img :src="coverPath" alt="">
    
   

    <h3 class="py-3"> <strong>Titolo: {{titolo}}</strong></h3>
    <h4>({{titoloOriginale}})</h4>
    <img class="w-25" v-bind:src="require ( '@/assets/'+ lingua)" alt="">
    <h5>Sigla Paese: {{paese}} </h5>
    <h5>Voto: {{voto}}</h5>
    <div class="py-3">
    <i class="fa fa-star fs-3 text-danger" v-for="(el,i) in calcStar" :key="'A'+ i"></i>
    <i class="fa fa-star-o fs-3 text-danger" v-for="(el,j) in (5 - calcStar)" :key="'B'+ j"></i>
    </div>
    
    
    <!-- Promemoria per il ciclo v-for e il warning in console
        
        https://stackoverflow.com/questions/51086657/vue-warn-duplicate-keys-detected-x-this-may-cause-an-update-error
     Same key for different v-for loops causing this warning.you can avoid this using different key for different v-for loops. -->
        
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

        calcStar(){

            const numStar = Math.ceil((this.voto / 2));

            return numStar;


        }
    },


}
</script>