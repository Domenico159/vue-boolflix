<template>
  <div class="colAttori">
      <!-- Movie -->
      <ul>
          <li @click="$emit('addActor',ele)"
          v-for="(ele,index) in filmsArray"
          :key="index">
              <img v-if="ele.profile_path != undefined" :src="`${urlImg}${ele.profile_path}`" alt="">
              <img v-else src="@/assets/img/poster-placeholder.png" alt="">
              <h2>{{ele.media_type == 'movie' ? ele.title : ele.name }}</h2>
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
    min-height: 450px;
    max-height: 450px;
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


         h2{
            color: $text-primary;
            position: absolute;
            font-size: 20px;
            top: 30px;
            left: 0px;
            padding: 5px;
            opacity: 0;
            min-width: 300px;
            }

            
            

      
       &:hover h2{
           animation: textEffect 0.5s forwards;
       }


       @keyframes textEffect {
                0%{
                    top: 30px;
                    opacity: 0;
                }

                100%{
                    top:-85px;
                    opacity: 1;
                    z-index: 10;
                }
       }
       

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