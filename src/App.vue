<template>
  <div id="app">
    <!-- Navbar -->
    <Navbar 
    @clickMovie="changeGender"
    @clickTv="changeGender"
    @clickBtn="thisTextClicked"
    @keyUp="thisTextClicked"
    />
   <Col :filmsArray="films"/>
  </div>
</template>

<script>
import Navbar from '@/components/Navbar.vue';
import Col from '@/components/Col.vue';
import axios from 'axios';

export default {
  name: 'App',
  components: {
    Navbar,
    Col,
  },
  data(){
    return {
      apiUrl:'https://api.themoviedb.org/3/search/movie?api_key=6425bcca50e476d0d6befdd1409e6aa5&language=it-IT',
      films:[],
      search:'all',
      thisTextClick:'',
    }
  },
  created(){
    this.getApi();
  },
  updated(){
    console.log(this.thisTextClick);
  },
  methods:{
    // Api
    getApi(){
      axios.get(this.apiUrl, {
    params: {
      query: this.search,
    }
   })
    .then((response) => {
      // handle success
      this.films = response.data.results;
    })
    .catch((error) => {
      // handle error
      console.log('Errore',error);
    });
        },
        // search BAR
        thisTextClicked(ele){
          if(!ele == ''){
            this.search = ele
            this.getApi();
          }else {
            this.search = 'all';
            this.getApi();
          }
        },

        changeGender(ele){
          let urlCustom = `https://api.themoviedb.org/3/search/${ele}?api_key=6425bcca50e476d0d6befdd1409e6aa5&language=it-IT`;
          this.apiUrl = urlCustom
          this.getApi();
        }
  
  },

}





</script>

<style lang="scss">
@import '@/style/vars';

*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app{
  max-height: 100vh;
  min-height: 100vh;
  background: $bg-color;
  padding:50px 10px 20px 10px;
  overflow-Y:auto ;
}
</style>
