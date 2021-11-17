<template>
  <div id="app">
    
    <CardContainer></CardContainer>

  </div>
</template>

<script>
import CardContainer from "./components/CardContainer.vue"

export default {
  name: 'App',
  components: {
   CardContainer,
  },

 
}
</script>

<style lang="scss">
@import "@/styles/generale.scss";


</style>
