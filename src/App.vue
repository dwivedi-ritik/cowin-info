<template>
  <div id="nav">
    <router-link to="/">Home</router-link> |
    <router-link to="/vaccine">Vaccine Info </router-link>|
    <router-link to="/about">About</router-link> 
  </div>
  <div id="ham-menu-p">
    <span class="material-icons" id="ham-menu" @click="hamToggle">
      menu  
    </span>
  </div>
  <div id="ham-route" v-if="showHamMenu">
    <router-link to="/" @click="hamToggle">Home</router-link> 
    <router-link to="/vaccine" @click="hamToggle">Vaccine Info </router-link>
    <router-link to="/about" @click="hamToggle">About</router-link>  
    <span class="material-icons" id="cross" @click="hamToggle">clear</span> 
  </div>
  <router-view/>
  <Footer />
</template>
<script>
import Footer from "./components/Footer"
export default {
  components:{Footer},
  data(){
    return{
      showHamMenu:true,
    }
  },
  methods:{
    hamToggle(){
      this.showHamMenu = !this.showHamMenu
    }
  }
}
</script>

<style>
#app {
  font-family:'Lato', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}
#ham-menu-p{
  display: none;
}
#ham-route a{
  text-decoration: none;
  font-size: 14px;
}
#ham-route{
  position:fixed;
  width: 0;
  z-index: 2;
  background-color: #fff;
  height: 300px;
  border-right: 1px rgba(0,0,0,0.1) solid;
  border-bottom: 1px rgba(0,0,0,0.1) solid;
  width: 120px;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
}

#ham-route a:hover{
  padding-left: 5%;
  transition:0.3s padding-left ease; 
}
#cross{
  font-size: 16px;
  position: absolute;
  top:5px;
  right:5px;
  cursor:pointer
}
#cross:hover{
  font-weight: bolder;
}
#nav {
  padding: 30px;
  font-size: 13px;
}
#nav a {
  color: #2c3e50;
  text-decoration: none;
  cursor:pointer;
}
#nav a.router-link-exact-active {
  background-color: blueviolet;
  padding: 7px;
  color:#fff;
  border-radius: 3px;
  opacity: 0.9;
}
#nav a.router-link-exact-active:hover{
  opacity: 1;
}

@media only screen and (max-width: 650px) {
  #ham-menu , #ham-menu-p{
    font-size: 32px;
    display: block;
  }
  #ham-menu-p{
    position: relative;
    width: 100vw;
    height: 40px;
    border-bottom: 1px rgba(0,0,0,0.1) solid;
  }
  .home{
    margin-top:5%;
  }
  #ham-menu{
    position: absolute;
    top:50%;
    left:2%;
    transform: translateY(-50%);
  }
  #ham-menu:hover{
    cursor:pointer;
    color:rgba(0,0,0,0.8);
  }
  #ham-route a:hover{
    font-weight: 600;
  }
  #nav{
    display: none;
  }
}
</style>
