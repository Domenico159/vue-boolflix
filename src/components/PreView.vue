<template>
  <div class="pre-view">
      <div class="text">
          <div class="info">
                  <h2>Titolo : {{genre == 'movie' ? poster.title : poster.name }}</h2>
                  <h2>Titolo originale : {{genre == 'movie' ? poster.original_title : poster.original_name }}</h2>
                  <img  v-if="poster.original_language == 'en'" src="@/assets/img/flags-boolflix/en.png" alt="">
                  <img  v-else-if="poster.original_language == 'it'" src="@/assets/img/flags-boolflix/it.png" alt="">
                  <h2 v-else>Lingua : {{poster.original_language}}</h2>
                 <div class="stars">
                      <i 
                  v-for="(e,index) in 5"
                  :key="index"
                  class="fas fa-star"
                  :class="{ 'active' : index <  Math.floor(poster.vote_average / 2)}"
                  ></i>
                  <div class="overview">
                  </div>
                 </div>
                 <div class="adult-or-child">
                     <i :class="{adult:poster.adult}"
                     class="fas fa-user-circle"></i>
                 </div>
                 <h2>Rilasciato il : {{ poster.release_date }}</h2>
                 <h2>Recensioni: {{ poster.popularity }}</h2>
                  </div>
                 <div class="descriptions">
                     <p>{{ poster.overview }}</p>
                 </div>
                 <div 
                 @click="$emit('clickIconAdd',poster)"
                 class="addListItem">
                 <i class="fas fa-plus"></i><span>Aggiungi alla lista</span>
                 </div>
      </div>
      <div class="imgPoster">
           <img :src="`${urlImg}${poster.poster_path}`" alt="">
      </div>
  </div>
</template>

<script>
export default {
    name:'PreView',
    props:['poster','genre'],
    data(){
        return {
            urlImg:'https://image.tmdb.org/t/p/original',
            language:'',
        }
    },
}
</script>

<style scoped lang="scss">
@import '@/style/vars';
.pre-view{
    min-height: 60vh;
    max-height: 60vh;
    overflow: hidden;
    display: flex;
    justify-content: space-between;
    padding: 5px;

    .text{
        color:$text-primary;
        width: 50%;
        position: relative;

        .addListItem{
            position: absolute;
            display: flex;
            align-items: center;
            right: 0;
            top: 20px;

            i{
                margin-right: 15px;
            }
             .fa-plus,
             span{
                 cursor: pointer;
             }

        }

         .info{
                min-height: 250px;
                padding-bottom: 10px;

            }

            .descriptions{
                margin:30px 20px ;
            }

            .fas {
                margin-right: 2px;
                font-size: 24px;
            }
            .fas.active{
                color: yellow;
                margin: 10px 0;
            }
            .fa-user-circle{
                color: rgb(81, 161, 27);
                margin: 10px 0;
            }
            .fa-user-circle.adult{
                color: rgb(161, 27, 27);
            }

            h2{
                font-size: 18px;
                margin-bottom: 10px;
            }
            img{
                width: 50px;
                height: 30px;
                margin-left: 10px;
                }
    }
    .imgPoster{
        width: 500px;
        max-height: 100%;
        padding-bottom: 5px;

        img{
            width: 100%;
            height: 100%;
            max-height: 100%;
            object-fit: cover;
        }
    }
}

</style>