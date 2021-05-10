<template>
  <div class="col">
      <ul>
          <li v-for="(ele,index) in filmsArray"
          :key="index">
              <img :src="`${urlImg}${ele.poster_path}`" alt="">
              <div class="overlay">
                  <h2>{{ele.title}}</h2>
                  <h2>{{ele.original_title}}</h2>
                  <img class="lan-en" v-if="ele.original_language == 'en'" src="@/assets/img/flags-boolflix/en.png" alt="">
                  <img  class="lan-it" v-else-if="ele.original_language == 'it'" src="@/assets/img/flags-boolflix/it.png" alt="">
                  <h2 v-else>{{ele.original_language}}</h2>
                  <h2>{{ele.vote_average}}</h2>
              </div>
          </li>
      </ul>
  </div>
</template>

<script>
export default {
    name:'Col',
    props:['filmsArray'],
    data(){
        return {
            urlImg:'https://image.tmdb.org/t/p/w342',
            language:'',
        }
    },
}
</script>

<style lang="scss" scoped>
@import '@/style/vars';
ul{
    display: flex;
    list-style: none;
    background: #fff;
    height: 350px;
    margin-top:30px ;
    overflow-X:auto ;

    li{
        margin-right: 10px;
        background: #ccc;
        max-height: 100%;
        min-width: 200px;
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

            h2{
                font-size: 18px;
                margin-bottom: 10px;
            }
            img.lan-en{
                width: 30px;
                height: 50px;
                transform: rotate(90deg);
            }
            img.lan-it{
                width: 50px;
                height: 30px;
            }
        }

        &:hover .overlay{
                visibility: visible;
            }
    }
}

</style>