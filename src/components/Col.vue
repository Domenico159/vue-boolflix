<template>
  <div class="col">
      <!-- Movie -->
      <ul>
          <li @click="$emit('addFilm',ele)"
          v-for="(ele,index) in filmsArray"
          :key="index">
              <img :src="`${urlImg}${ele.poster_path}`" alt="">
          </li>
      </ul>
  </div>
</template>

<script>
export default {
    name:'Col',
    props:['filmsArray','genre'],
    data(){
        return {
            urlImg:'https://image.tmdb.org/t/p/original',
            language:'',
        }
    },
    methods:{
        activeInfoClick(){
            this.activeInfo = ! this.activeInfo
        }
    },
}
</script>

<style lang="scss" scoped>
@import '@/style/vars';

ul{
    display: flex;
    list-style: none;
    min-height: 350px;
    max-height: 350px;
    margin-top: 30px;
    overflow-x: auto;
    align-items: center;
   

    li{
        min-width: calc(100% / 8 - 10px);
        max-width: calc(100% / 8 - 10px);
        position: relative;
        cursor: pointer;
        margin: 20px 5px;
        height: 220px;
       

        &:hover img{
            position: relative;
            transform: scale(1.4);
            z-index: 9;
            height: auto;
            
            
        }
        img{
            max-height: 100%;
            width: 100%;
            object-fit: cover;
             transition: all 0.3s;
              border-radius: 20%;
        }
    }

}

</style>