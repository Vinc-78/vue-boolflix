<template>

<li class="fs-3"> {{titolo}} - ({{titoloOriginale}}) - {{lingua}} - {{voto}}</li>

  
</template>

<script>
export default {
    name: "SingolCard",

    props:{
        titolo: String,
        titoloOriginale: String,
        lingua: String,
        voto: Number
    }


}
</script>