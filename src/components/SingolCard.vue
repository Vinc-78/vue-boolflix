<template>


<div class="text-center">

    <div class="card-singola">

    
    <img :src="coverPath" alt="">
    

    <div class="overlay">

    <h3 class="py-5" > <strong>{{titolo}}</strong></h3>
    <h4 v-if="titolo !== titoloOriginale">{{titoloOriginale}}</h4>
    <img class="w-25" v-bind:src="require ( '@/assets/'+ lingua)" alt="">
   <!--  <h5>Sigla Paese: {{paese}} </h5>
    <h5>Voto: {{voto}}</h5> -->
    <div class="py-3">
    <i class="fa fa-star fs-3 text-white" v-for="(el,i) in calcStar" :key="'A'+ i"></i>
    <i class="fa fa-star-o fs-3 text-white" v-for="(el,j) in (5 - calcStar)" :key="'B'+ j"></i>
    </div>

    <h3 v-if="this.nomegeneri.length>0">Generi: {{nomegeneri.toString()}}</h3>

    <h4 v-if="trama!=''">Trama</h4>
    <span class="fs-5">{{trama}}</span>
  </div>

    
   

    
    </div>
    
    
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
        cover: {String},
        trama:{String},
        cardgeneri:{Array},
        allgenere:{Array}
        
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


        },
        nomegeneri(){

            let nomigenCard =[];

            for(let i=0; i<this.cardgeneri.length; i++){
                for(let j=0; j<this.allgenere.length; j++){
                    if( this.cardgeneri[i]===this.allgenere[j].id){
                        nomigenCard.push(this.allgenere[j].name)
                    }

                }
                

            }
            return nomigenCard
        }
    },


}
</script>