<template>
  <nav>
      <div class="logo">
          <img src="../assets/img/logoNetflix.png" alt="">
          <div class="type">
              <span @click="$emit('clickHome','home')"
              >Home</span>
              <span @click="$emit('clickMovie','movie')"
              >Films</span>
              <span  @click="$emit('clickTv','serie-TV')"
              >Serie Tv</span>
          </div>
      </div>
      <div class="search">
          <span>Search:</span>
          <input placeholder="Search:"
           @keyup="$emit('keyUp', searchText)"
          v-model="searchText" text="">
          <input @click="$emit('clickBtn', searchText)"
          class="btn" type="button" value="Cerca">
      </div>
  </nav>
</template>

<script>
export default {
   name:'Navbar',
   data(){
       return {
           searchText:'',
       }
   },
}
</script>

<style lang="scss" scoped>
@import '@/style/vars';
nav{
    position: fixed;
    height: 50px;
    top: 0;
    left: 0;
    right: 0;
    z-index: 10;
    background: $bg-navbar;
    display: flex;
    align-items: center;
    justify-content: space-between;

    .logo{

        display: flex;
        align-items: center;

        img{
        width: 150px;
        margin-top:5px ;
        margin-left: 10px;
        margin-right: 40px;
    }
       .type{
           color: $text-primary;

           span{
               margin-right: 20px;
               cursor: pointer;
           }
       }
    } 
    
    .search{
        margin-right: 50px;

        .btn{
            margin-left: 20px;
        }

        span{
            color: $text-primary;
            margin-right: 10px;
        }
    }
}
</style>