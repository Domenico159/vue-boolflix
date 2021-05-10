<template>
  <div class="col">
      <ul>
          <li v-for="(ele,index) in filmsArray"
          :key="index">
              <img :src="`${urlImg}${ele.poster_path}`" alt="">
              <div class="overlay">
                  <h2>{{ele.title}}</h2>
                  <h2>{{ele.original_title}}</h2>
                  <h2>{{ele.original_language}}</h2>
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
        }

        &:hover .overlay{
                visibility: visible;
            }
    }
}

</style>