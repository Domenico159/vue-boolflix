<template>
  <div class="pre-view-attori">
      
      
  </div>
</template>

<script>
export default {
    name:'PreViewAttori',
    props:['poster','genre','effectAdd'],
    data(){
        return {
            urlImg:'https://image.tmdb.org/t/p/original',
            language:'',
            statusTextEffect:false,
        }
    },
}
</script>

<style scoped lang="scss">
@import '@/style/vars';


.pre-view-attori{
    min-height: 70vh;
    max-height: 70vh;
    overflow: hidden;
    display: flex;
    justify-content: space-around;
    padding: 20px 5px 5px 5px;
    margin-top: 30px;
}

</style>