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
    background: rgb(88, 88, 88);
    height: 200px;
    max-height: 200px;
    margin-top: 10px;
    overflow-X:auto ;

    li{
        background: #ccc;
        max-height: 100%;
        min-width: 200px;
        max-width: 200px;
        position: relative;
        overflow: hidden;
        cursor: pointer;

        &:hover img{
            transform: scale(1.2);
        }
        img{
            max-height: 100%;
            width: 100%;
            object-fit: cover;
             transition: transform 0.3s;
        }
    }

}

</style>