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
              <span>Nuovi e popolari</span>
              <span>La mia lista</span>
          </div>
      </div>
      <div class="search">
          <span><i @click="clickSearch"
          class="fas fa-search"></i></span>
          <input :class="{in:iconStatus, out:!iconStatus}"
          class="text"
           placeholder="Search:"
           @keyup="$emit('keyUp', searchText)"
          v-model="searchText" text="">
          <div class="notifiche">
              <i class="fas fa-bell"></i>
              <i class="fas fa-gift"></i>
          </div>
          <div class="user">
          <img src="@/assets/img/Netflix-avatar.png" alt="">
          <i class="fas fa-caret-down"></i>
      </div>
      </div>
  </nav>
</template>

<script>
export default {
   name:'Navbar',
   data(){
       return {
           searchText:'',
           iconStatus:false,
       }
   },
   methods:{
       clickSearch(){
           this.iconStatus = !this.iconStatus
       }
   },
}
</script>

<style lang="scss" scoped>
@import '@/style/vars';
nav{
    position: fixed;
    height: 70px;
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
        display: flex;
        align-items: center;
        align-content: flex-start;
        color: $text-primary;


        .notifiche{
            margin-left: 30px;
            font-size: 20px;

            i{
                margin: 0 10px;
                cursor: pointer;
            }
        }

        .fa-search{
            cursor: pointer;
        }

        span{
            color: $text-primary;
            margin-right: 10px;
        }

        .text{
            background: transparent;
            border:none;
            border-bottom: 1px solid #ccc;
            height: 30px;
            width: 0px;
        }

        .text.in{
            animation: search-in 1s forwards;
        }

        .text.out{
            animation: search-out 1s forwards;
        }

        @keyframes search-in {
            0%{
                width: 0px;
            }

            100%{
                width: 200px;
                padding: 5px 10px;
            }
        }

         @keyframes search-out {
            0%{
                width: 200px;
                padding: 5px 10px;
            }

            100%{
               width: 0px;
            }
        }

        .user{

            display: flex;
            align-items: center;
            img{
                width: 35px;
                margin-left: 50px;
                margin-right: 10px;
                cursor: pointer;
            }

            i{
                transform: translateY(2px);
                cursor: pointer;
            }
        }

    }
}
</style>