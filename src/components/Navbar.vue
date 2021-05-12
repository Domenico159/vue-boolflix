<template>
  <nav @mouseenter="navResIn"
       @mouseleave="navResOut"
  >
      <div class="logo">
          <img src="../assets/img/logoNetflix.png" alt="">
          <div class="type">
              <span @click="$emit('clickHome','home')"
              >Home</span>
              <span @click="$emit('clickMovie','movie')"
              >Films</span>
              <span  @click="$emit('clickTv','serie-TV')"
              >Serie Tv</span>
              <span  @click="$emit('clickList','list')"
              >La mia lista</span>
          </div>
      </div>
      <div class="search">
          <span><i @click="clickSearch"
          class="fas fa-search"></i></span>
          <input :class="{in:iconStatus, out:iconStatus == false}"
          class="text"
           placeholder="Search:"
           @keyup="$emit('keyUp', searchText)"
          v-model="searchText" text="">
          <div class="notifiche">
              <i class="fas fa-bell"></i>
              <i class="fas fa-gift"></i>
          </div>
          <div @click="infoUser"
          class="user">
          <img src="@/assets/img/Netflix-avatar.png" alt="">
          <i :class="{in:clickInfoUser, out:!clickInfoUser}"
          class="fas fa-caret-down"></i>
          <ul v-if="clickInfoUser">
              <li>
                   <img src="@/assets/img/Netflix-avatar.png" alt="">
                   <span>Domenico</span>
              </li>
              <li>
                  <span>Gestisci i profili</span>
              </li>
              <li class="options">
                  <span>Account</span>
                  <span>Centro assistenza</span>
                  <span>Esci da Netflix</span>
              </li>
          </ul>
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
           iconStatus:undefined,
           clickInfoUser:false,
       }
   },
   methods:{
       clickSearch(){
           this.iconStatus = !this.iconStatus
       },
       infoUser(){
           this.clickInfoUser = !this.clickInfoUser
       },
       navResOut(){
           if(this.iconStatus){
               this.iconStatus = false
               this.searchText = ''
           }
       },
        navResIn(){
           this.iconStatus = undefined
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
    background: rgba($bg-navbar,1);
    box-shadow: 10px 0px 10px #000;
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
               border-bottom: 3px solid transparent;

               &:hover{
                   animation: border-in 0.6s forwards;
               }

               @keyframes border-in {
                   
                   0%{
                       padding-bottom: 0px;
                       border-color:#db1927 ;
                   }

                   100%{
                       padding-bottom: 25px;
                       border-color:#db1927 ;
                   }
               }
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
            transition: color 0.3s;
        }

        .text{
            background: transparent;
            border:none;
            border-bottom: 1px solid #ccc;
            height: 30px;
            width: 0px;
            color: $text-primary;
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
            position: relative;

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

            i.in{
                 animation: clickInfo-in 0.5s forwards;
            }

            i.out{
                 animation: clickInfo-out 0.5s forwards;
            }

            @keyframes clickInfo-in {
                0%{
                    transform: rotate(0);
                }

                100%{
                    transform: rotate(-180deg);
                }
            }

            @keyframes clickInfo-out {
                0%{
                    transform: rotate(-180deg);
                }

                100%{
                    transform: rotate(0);
                }
            }

           ul{
               position: absolute;
               bottom: -280px;
               right: 10px;
               list-style: none;
               display: flex;
               flex-direction: column;
               align-items: center;
               background: rgba($bg-color,0.9);
               width: 180px;
               padding: 20px 5px;
               box-shadow: 5px 5px 15px #000;

               li{
                   display: flex;
                   margin-bottom: 15px;
                   align-items: center;

                   span{
                       cursor: pointer;
                       margin-bottom: 10px;

                       &:hover{
                           color: #0d7e80;
                       }
                   }

                   img{
                       width: 35px;
                       margin: 0 10px 0 0 ;
                   }
                   
               }


               li.options{
                   flex-direction: column;
                   padding-top: 30px;
                   border-top:1px solid #ccc;
                   align-items: flex-start;
               }
               
           }
        }

    }
}
</style>