<template>

<li class="fs-3"> {{titolo}} - ({{titoloOriginale}}) -{{voto}} - <img class="w-25" v-bind:src="require ( '@/assets/'+ lingua)" alt=""></li>

 
</template>

<script>
export default {
    name: "SingolCard",

    props:{
        titolo: {String},
        titoloOriginale: { String},
        lingua: {Image,
                default:() => "mondo.png"},
        voto: {Number}
    }


}
</script>