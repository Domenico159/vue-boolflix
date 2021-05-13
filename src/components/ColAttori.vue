<template>
  <div class="colAttori">
      <!-- Movie -->
      <ul>
          <li @click="$emit('addActor',ele)"
          v-for="(ele,index) in filmsArray"
          :key="index">
              <img v-if="ele.profile_path != undefined" :src="`${urlImg}${ele.profile_path}`" alt="">
              <img v-else src="@/assets/img/poster-placeholder.png" alt="">
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
    padding: 0px 20px;
   

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