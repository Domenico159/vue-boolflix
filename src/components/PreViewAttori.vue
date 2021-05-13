<template>
  <div class="pre-view-attori">
      <section>
       <h1>{{ poster.name }}</h1>
      <div class="imgPoster">
      <img v-if="poster.profile_path != undefined" :src="`${urlImg}${poster.profile_path}`" alt="">
      <img v-else src="@/assets/img/poster-placeholder.png" alt="">
      </div>
      </section>
      <h2>Film : </h2>
      <div class="colAttori">

           <ul>
          <li @click="addPoster(ele)"
          v-for="(ele,index) in poster.known_for"
          :key="index">
              <img v-if="ele.poster_path != undefined" :src="`${urlImg}${ele.backdrop_path}`" alt="">
              <img v-else src="@/assets/img/poster-placeholder.png" alt="">
              <h2>{{ele.media_type == 'movie' ? ele.title : ele.name }}</h2>
          </li>
      </ul>
      </div>

      <PreViewFilmAttori v-if=" thisPoster.length != 0 "
    :poster="thisPoster"
     />


  </div>
</template>

<script>
import PreViewFilmAttori  from '@/components/PreViewFilmAttori.vue';
export default {
    name:'PreViewAttori',
    components:{
        PreViewFilmAttori ,
    },
    props:['poster','genre','effectAdd'],
    data(){
        return {
            urlImg:'https://image.tmdb.org/t/p/original',
            language:'',
            statusTextEffect:false,
            thisPoster:[],
            thisFilmActor:[],
        }
    },
    methods:{
        addPoster(ele){
            this.thisPoster = ele
            console.log(ele);
        },
    },
}
</script>

<style scoped lang="scss">
@import '@/style/vars';


.pre-view-attori{
    min-height: 100vh;
    overflow: hidden;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 20px 5px 5px 5px;
    margin-top: 30px;
    color:$text-primary;


    ul{
    display: flex;
    justify-content: center;
    list-style: none;
    min-height: 450px;
    max-height: 450px;
    margin-top: 30px;
    overflow-x: auto;
    align-items: center;
    padding: 0px 100px;

    li{
        min-width: 350px;
        max-width: 350px;
        position: relative;
        cursor: pointer;
        margin: 20px 5px;
        height: 300px;


        
         h2{
            color: $text-primary;
            position: absolute;
            font-size: 20px;
            top: 30px;
            left: -120px;
            opacity: 0;
            min-width: 800px;
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
                    top:-68px;
                    opacity: 1;
                    z-index: 8;
                }
       }
       

        &:hover img{
            position: relative;
            transform: scale(1.3);
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


    h1{
        margin-bottom: 15px;
        text-align: center;
        font-size: 30px;
    }

    h2{
       align-self: flex-start;
       margin-left: 100px;
       font-size: 28px;
    }

   .imgPoster{
        width: 300px;
        max-height: 100%;
        padding-bottom: 5px;
        overflow: hidden;

        img{
            width: 100%;
            height: auto;
            max-height: 100%;
            object-fit: cover;
            border-radius: 20px;
        }
    }
}

</style>