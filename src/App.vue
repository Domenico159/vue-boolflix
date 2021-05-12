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

    <PreView @clickIconAdd="clickedAdd"
     :genre="thisGenre"
    :poster="thisPoster"
     v-if="!myListActive"
     />

    <div v-if="!myListActive" class="normal">
   <Col @addFilm="addFilms"
   v-if="libreria != 'home'" :genre="thisGenre"
   :filmsArray="films"/>

   <div v-else class="home">
     <Col @addFilm="addFilms"
     :genre="thisGenre"
     :filmsArray="home"/>
   </div>
    </div>

   <div v-else
   class="myList">
   <h1 v-if="!myList.length == 0"
   >La tua lista</h1>
   <h1 v-else
   >Non hai scelto film da salvare</h1>
   <Mylist @removeItemList="removeListItem"
   :genre="thisGenre"
   :listItem="myList"
   />
   </div>

   
  </div>
</template>

<script>
import Navbar from '@/components/Navbar.vue';
import Col from '@/components/Col.vue';
import Mylist from '@/components/Mylist.vue';
import PreView from '@/components/PreView.vue';
import axios from 'axios';

export default {
  name: 'App',
  components: {
    Navbar,
    Col,
    Mylist,
    PreView,
  },
  data(){
    return {
      apiUrl:'https://api.themoviedb.org/3/search/movie?api_key=6425bcca50e476d0d6befdd1409e6aa5&language=it-IT',
      apiHome1:'https://api.themoviedb.org/3/search/movie?api_key=6425bcca50e476d0d6befdd1409e6aa5&query=a&language=it-IT',
      apiSerie:'https://api.themoviedb.org/3/search/tv?api_key=6425bcca50e476d0d6befdd1409e6aa5&query=all&language=it-IT',
      films:[],
      home:[],
      serie:[],
      myList:[],
      search:'all',
      thisTextClick:'',
      thisGenre:'movie',
      libreria:'home',
      myListActive:false,
      thisPoster:[],
    }
  },
  created(){
    this.getApi();
    this. getHome()
    this.getSerie()
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
      console.log('Errore 1',error);
    });
        },


        getHome(){

            axios.get(this.apiHome1)

            .then( result => {
                this.home = result.data.results
                this.thisPoster = this.home[0]
            })

            .catch(err =>{
                console.log(err);
            })

        },
        getSerie(){

            axios.get(this.apiSerie)

            .then( result => {
                this.serie = result.data.results
            })

            .catch(err =>{
                console.log(err);
            })

        },
        clickedAdd(ele){
          if(!this.myList.includes(ele)){
            this.myList.push(ele)
          }
        },
        addFilms(ele){
          this.thisPoster = ele
        },

        removeListItem(index){
          this.myList.splice(index,1)
        },



        // search BAR
        thisTextClicked(ele){
          if(!ele == ''){
            this.search = ele
              this.getApi()
            if(this.libreria == 'home'){
               this.libreria = 'movie'
            }
          }else {
            this.search = 'all';
            this.getApi();
          }
        },

        selectPoster(){
          if(this.libreria == 'movie'){
            this.thisPoster = this.films[0]

          } else if(this.libreria == 'serie-TV'){
            this.thisPoster = this.serie[0]

          }else if (this.libreria == 'home') {
            this.thisPoster = this.home[0]
          }
        },

        changeGender(ele){
          if(ele == 'movie'){
            this.libreria = 'films';
            console.log('1',this.libreria);
            this.thisGenre = 'movie'
            let urlCustom = `https://api.themoviedb.org/3/search/${this.thisGenre}?api_key=6425bcca50e476d0d6befdd1409e6aa5&language=it-IT`;
            this.apiUrl = urlCustom
            this.getApi();
            this.myListActive = false;
            console.log('2',this.libreria);

          } else if(ele == 'serie-TV'){
            this.thisGenre = 'tv'
            let urlCustom = `https://api.themoviedb.org/3/search/${this.thisGenre}?api_key=6425bcca50e476d0d6befdd1409e6aa5&language=it-IT`;
            this.apiUrl = urlCustom
            this.getSerie();
            this.libreria = 'serie-TV';
            this.myListActive = false;
            this.films = this.serie

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

          this.selectPoster()
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
  padding:80px 10px 50px 10px;
  overflow-X: hidden;
  overflow-Y: auto;

  h1{
    color: $text-primary;
    text-transform: capitalize;
    margin-top: 10px;
  }
}
</style>
