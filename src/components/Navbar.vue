<template>
  <nav>
      <div class="logo">
          <img src="../assets/img/logoNetflix.png" alt="">
      </div>
      <div class="search">
          <input @keyup="$emit('keyUp', searchText)"
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

    .logo img{
        width: 150px;
        margin-top:5px ;
        margin-left: 10px;
    }

    .search{
        margin-right: 50px;

        .btn{
            margin-left: 20px;
        }
    }
}
</style>