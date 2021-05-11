<template>
  <div class="col">
      <!-- Movie -->
      <ul>
          <li
          v-for="(ele,index) in filmsArray"
          @click="$emit('addFilm',ele)"
          :key="index">
              <img :src="`${urlImg}${ele.poster_path}`" alt="">
              <div class="overlay">
                  <div class="info">
                      <h2>{{genre == 'movie' ? ele.title : ele.name }}</h2>
                  <h2>{{genre == 'movie' ? ele.original_title : ele.original_name }}</h2>
                  <img  v-if="ele.original_language == 'en'" src="@/assets/img/flags-boolflix/en.png" alt="">
                  <img  v-else-if="ele.original_language == 'it'" src="@/assets/img/flags-boolflix/it.png" alt="">
                  <h2 v-else>{{ele.original_language}}</h2>
                 <div class="stars">
                      <i 
                  v-for="(e,index) in 5"
                  :key="index"
                  class="fas fa-star"
                  :class="{ 'active' : index <  Math.floor(ele.vote_average / 2)}"
                  ></i>
                  <div class="overview">
                  </div>
                 </div>
                 <div class="adult-or-child">
                     <i :class="{adult:ele.adult}"
                     class="fas fa-user-circle"></i>
                 </div>
                 <h2>Rilasciato il {{ ele.release_date }}</h2>
                 <h2>Recensioni: {{ ele.popularity }}</h2>
                  </div>
                 <div class="descriptions">
                     <p>{{ ele.overview }}</p>
                 </div>
                 <div class="addListItem">
                 <i class="fas fa-plus"></i><span>Aggiungi alla lista</span>
                 </div>
              </div>
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
    height: 400px;
    margin-top:30px ;
    overflow-X:auto ;

    li{
        margin-right: 10px;
        background: #ccc;
        max-height: 100%;
        min-width: 280px;
        position: relative;
        overflow: hidden;
        cursor: pointer;
        img{
            height: 100%;
            width: 100%;
            object-fit: cover;
        }
        .overlay{
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0,0,0,0.8);
            visibility: hidden;
            color: $text-primary;
            padding: 10px;
            display: flex;
            flex-direction: column;
            overflow-y: auto;
            min-height: 100%;
            max-height: 100%;

            .addListItem{
                text-align: center;
                display: flex;
                align-items: center;
                justify-content: center;
                margin-bottom: 20px;

                i{
                    margin-right: 15px;
                }
            }

            h2.addList{
                margin-bottom: 30px;
            }

            .info{
                min-height: 250px;
                display: flex;
                flex-direction: column;
                align-items: center;
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

        &:hover .overlay{
                visibility: visible;
            }
    }

}

</style>