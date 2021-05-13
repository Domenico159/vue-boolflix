<template>
  <div class="pre-view">
      <div class="text">
          <div class="info">
                  <h1>{{poster.media_type == 'movie' ? poster.title : poster.name }}</h1>
                  <h2>{{poster.media_type == 'movie' ? poster.original_title : poster.original_name }}</h2>
                  <img  v-if="poster.original_language == 'en'" src="@/assets/img/flags-boolflix/en.png" alt="">
                  <img  v-else-if="poster.original_language == 'it'" src="@/assets/img/flags-boolflix/it.png" alt="">
                  <h2 v-else>Lingua : {{poster.original_language}}</h2>
                 <div class="recensioni">
                     <div class="stars">
                      <i 
                  v-for="(e,index) in 5"
                  :key="index"
                  class="fas fa-star"
                  :class="{ 'active' : index <  Math.floor(poster.vote_average / 2)}"
                  ></i>
                 </div>
                  <h2>{{ poster.popularity }}</h2>
                  <div class="like">
                     <i class="fas fa-thumbs-up"></i>
                     <i class="fas fa-thumbs-down"></i>
                 </div>
                 <div 
                 @click="$emit('clickIconAdd',poster)"
                 class="addListItem">
                 <i 
                 class="fas fa-plus"></i><span>Aggiungi alla lista</span>
                 <span :class="{in:effectAdd}"
                 class="addText">Aggiunto</span>
                 </div>
                 </div>
                 <h2 v-if="genre != 'home'" class="mediaType">{{ genre }}</h2>
                 <h2 v-else class="mediaType">{{ poster.media_type }}</h2>
                 <div class="adult-or-child">
                     <i :class="{adult:poster.adult}"
                     class="fas fa-user-circle"></i>
                 </div>
                 <h2>{{ poster.release_date }}</h2>
                 <div class="descriptions">
                     <p>{{ poster.overview }}</p>
                 </div>
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
.pre-view{
    min-height: 70vh;
    max-height: 70vh;
    overflow: hidden;
    display: flex;
    justify-content: space-around;
    padding: 20px 5px 5px 5px;

    .text{
        color:$text-primary;
        width: 50%;
        position: relative;
        overflow-y: auto;

        .mediaType{
                background: brown;
                padding: 5px;
                border-radius:10px ;
                min-width: 40px;
                text-align: center;
                max-width: 80px;
                text-transform: uppercase;
            }

        .like{
            display: flex;
            align-items:center ;
            margin-left: 40px;

            .fa-thumbs-up{
                color: rgb(15, 172, 15);
                
            }

            .fa-thumbs-down{
                color:#db1927 ;
            }
            i{
                margin-right: 30px;
                font-size: 24px;
                cursor: pointer;
            }
        }

        .recensioni{
            display: flex;
            align-items: center;
            margin-bottom: 15px;


            h2{
                transform: translateY(10px);
                margin-left: 15px;
            }
        }

        h1{
            margin-bottom: 10px;
        }

        

        .addListItem{
            position: absolute;
            display: flex;
            align-items: center;
            right: 50px;
            top: 100px;

            .addText{
                position: absolute;
                bottom: 0px;
                color:#db1927 ;
                right: 30px;
                font-weight: 600;
                font-size: 28px;
                display: inline-block;
                visibility: hidden;
            }

            .addText.in{
                animation: addTextEffect-in 1.5s forwards;
            }

            @keyframes addTextEffect-in  {
                0%{
                    bottom: 0px;
                    visibility: visible;
                }

                90%{
                    bottom: 50px;
                }
                100%{
                    visibility: hidden;
                    opacity: 0;
                }
            }
            

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
                font-size: 20px;
            }
            .fas.active{
                color: #db1927;
                margin: 10px 0;
            }
            .fa-user-circle{
                color: rgb(15, 172, 15);
                margin: 10px 0;
                position: absolute;
                right: 20px;
                top: 10px;
                font-size: 28px;
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
        width: 300px;
        max-height: 100%;
        padding-bottom: 5px;
        overflow: hidden;
        border-radius: 20px;

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