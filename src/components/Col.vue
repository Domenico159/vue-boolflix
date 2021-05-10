<template>
  <div class="col">
      <ul>
          <li v-for="(ele,index) in filmsArray"
          :key="index">
              <img src="" alt="">
              <h1>{{ ele.original_title }}</h1>
              <p>{{ ele.overview}}</p>
          </li>
      </ul>
  </div>
</template>

<script>
export default {
    name:'Col',
    props:['filmsArray'],
    updated(){
        console.log(this.filmsArray);
    }
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
        height: 100%;
        min-width: 200px;
    }
}

</style>