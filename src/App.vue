<template>
  <div id="app">
    <!-- Navbar -->
    <Navbar 
    @clickMovie="changeGender"
    @clickTv="changeGender"
    @clickHome="changeGender"
    @clickBtn="thisTextClicked"
    @keyUp="thisTextClicked"
    @clickList="changeGender"
    />

    <div v-if="!myListActive" class="normal">
      <h1>{{ libreria }}</h1>

   <Col @addFilm="addFilms"
   v-if="libreria != 'home'" :genre="thisGenre"
   :filmsArray="films"/>

   <div v-else class="home">
     <Col @addFilm="addFilms"
     :genre="thisGenre"
     :filmsArray="home1"/>

   <Col  @addFilm="addFilms"
    :genre="thisGenre"
   :filmsArray="home2"/>

   <Col @addFilm="addFilms"
    :genre="thisGenre"
   :filmsArray="home3"/>


   <Col @addFilm="addFilms"
    :genre="thisGenre"
   :filmsArray="home4"/>
   </div>
    </div>

   <div v-else
   class="myList">
   <h1 v-if="!myList.length == 0"
   >My list</h1>
   <h1 v-else
   >Non hai scelto film da salvare</h1>
     <Col @addFilm="addFilms"
     :genre="thisGenre"
   :filmsArray="myList"/>
   </div>

   
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
      apiHome1:'https://api.themoviedb.org/3/search/movie?api_key=6425bcca50e476d0d6befdd1409e6aa5&query=a&language=it-IT',
      apiHome2:'https://api.themoviedb.org/3/search/movie?api_key=6425bcca50e476d0d6befdd1409e6aa5&query=b&language=it-IT',
      apiHome3:'https://api.themoviedb.org/3/search/movie?api_key=6425bcca50e476d0d6befdd1409e6aa5&query=c&language=it-IT',
      apiHome4:'https://api.themoviedb.org/3/search/movie?api_key=6425bcca50e476d0d6befdd1409e6aa5&query=d&language=it-IT',
      films:[],
      home1:[],
      home2:[],
      home3:[],
      home4:[],
      myList:[],
      search:'all',
      thisTextClick:'',
      thisGenre:'movie',
      libreria:'home',
      myListActive:false,
    }
  },
  created(){
    this.getApi();
    this. getHome()
    this. getHome1()
    this. getHome2()
    this. getHome3()
  },
  updated(){

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


        getHome(){

            axios.get(this.apiHome1)

            .then( result => {
                this.home1 = result.data.results
            })

            .catch(err =>{
                console.log(err);
            })

        },

        getHome1(){

            axios.get(this.apiHome2)

            .then( result => {
                this.home2 = result.data.results
            })

            .catch(err =>{
                console.log(err);
            })

        },

        getHome2(){

            axios.get(this.apiHome3)

            .then( result => {
                this.home3 = result.data.results
            })

            .catch(err =>{
                console.log(err);
            })

        },

        getHome3(){

            axios.get(this.apiHome4)

            .then( result => {
                this.home4 = result.data.results
            })

            .catch(err =>{
                console.log(err);
            })

        },
        
        addFilms(ele){
          if(!this.myList.includes(ele)){
            this.myList.push(ele)
          }
        },



        // search BAR
        thisTextClicked(ele){
          if(!ele == ''){
            this.search = ele
            this.getApi();
            if(this.libreria == 'home'){
               this.libreria = 'movie'
            }
          }else {
            this.search = 'all';
            this.getApi();
          }
        },

        changeGender(ele){

          if(ele == 'movie'){
            this.thisGenre = 'movie'
            let urlCustom = `https://api.themoviedb.org/3/search/${ this.thisGenre}?api_key=6425bcca50e476d0d6befdd1409e6aa5&language=it-IT`;
            this.apiUrl = urlCustom
            this.getApi();
            this.libreria = 'films';
            this.myListActive = false;

          } else if(ele == 'serie-TV'){
            this.thisGenre = 'tv'
            let urlCustom = `https://api.themoviedb.org/3/search/${this.thisGenre}?api_key=6425bcca50e476d0d6befdd1409e6aa5&language=it-IT`;
            this.apiUrl = urlCustom
            this.getApi();
            this.libreria = 'serie-TV';
            this.myListActive = false;

          }else if (ele == 'home') {
            this.thisGenre = 'movie'
            let urlCustom = `https://api.themoviedb.org/3/search/${this.thisGenre}?api_key=6425bcca50e476d0d6befdd1409e6aa5&language=it-IT`;
            this.apiUrl = urlCustom
            this.getApi();
            this.libreria = 'home';
            this.myListActive = false;
          } else if (ele == 'list'){
            this.myListActive = !this.myListActive
          }
        },
  
  },

}


</script>

<style lang="scss">
@import '@/style/vars';

*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: $main-font;
}


/* Custom scrollbar */

/* width */
::-webkit-scrollbar {
    width: 15px;
    height: 15px;
  }
  
  /* Track */
  ::-webkit-scrollbar-track {
    box-shadow: inset 0 0 5px rgba(124, 124, 124,0.4);
    border-radius: 10px;
  }
  
  /* Handle */
  ::-webkit-scrollbar-thumb {
    background: #0d7e80;
    border-radius: 10px;
  }

#app{
  max-height: 100vh;
  min-height: 100vh;
  background: $bg-color;
  padding:80px 10px 20px 10px;
  overflow-Y:auto ;

  h1{
    color: $text-primary;
    text-transform: capitalize;
    margin-top: 10px;
  }
}
</style>
