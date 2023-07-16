<template>
  <div class="nav" :class="{'nav nav_black' : Show  }">
      <img
            class="nav_logo"
            src="https://upload.wikimedia.org/wikipedia/commons/thumb/0/08/Netflix_2015_logo.svg/250px-Netflix_2015_logo.svg.png"
            alt="Netflix Logo"
          />
          <img
            class="nav_avatar"
            src="https://mir-s3-cdn-cf.behance.net/project_modules/disp/366be133850498.56ba69ac36858.png"
            alt="Netflix Logo"
          />
        </div>
</template>

<script>
import { ref,watch,watchEffect } from 'vue'
export default {
    setup(){
        let Show = ref(false)
        watchEffect(()=>{
          window.addEventListener("scroll", () => { 
              if (window.scrollY > 100) {
              Show.value = true
             }else{
              Show.value= false
             }
          })
           return () => {
        window.removeEventListener("scroll")
      }
        });
        
        return{Show}
    }
}
</script>

<style>
.nav {
  position: fixed;
  top: 0;
  width: 100%;
  padding: 20px;
  height: 30px;
  z-index: 1;

  
  display: flex;
  justify-content: space-between;
  /* Animation */
  transition-timing-function: ease-in;
  transition: all 0.5s;

}

.nav_black {
 background-color: #111 !important;
}
.test1{
    background-color: aqua;
}
.test2{
    background-color: darkgreen !important;
}

.nav_logo {
  position: fixed;
  left: 20px;
  width: 80px;
  object-fit: contain;
}

.nav_avatar {
  position: fixed;
  right: 20px;
  width: 30px;
  object-fit: contain;
}
</style>    