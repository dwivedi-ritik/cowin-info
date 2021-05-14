<template>
  <div id="nav">
    <router-link to="/">Home</router-link> |
    <router-link to="/vaccine">Vaccine Info </router-link>|
    <router-link to="/about">About</router-link> 
  </div>
  <router-view/>
  <Footer />

</template>
<script>
import Footer from "./components/Footer"
export default {
  components:{Footer}
}
</script>

<style>
#app {
  font-family:'Lato', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
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
</style>
