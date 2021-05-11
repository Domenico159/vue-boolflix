<template>
  <div class="myList">

      <div class="all-box" v-for="(ele,index) in listItem"
      :key="index">
       <div @click="$emit('removeItemList',index)"
       class="remove">
           <i class="fas fa-minus-circle"></i>
       </div>
      <div class="content box">
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
              </div>
      </div>
      </div>

  </div>
</template>

<script>
export default {

    name:'Mylist',
    props:['listItem','genre'],
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

.myList{
    display: flex;
    flex-wrap: wrap;
    min-height: 100vh;
    padding: 20px 10px;

    .all-box{
        position: relative;
        max-width: calc(100% / 4 - 20px);
     
    }

    .fa-minus-circle{
        position: absolute;
        top:5px;
        left: 0px;
        color: rgb(202, 24, 24);
        z-index: 8;
        font-size: 22px;
        cursor: pointer;
    }

    .box{
        background: #000;
        height: 500px;
        margin: 20px 10px;
        margin-right: 10px;
        background: #ccc;
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