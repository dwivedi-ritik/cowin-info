<template>
  <div id="nav">
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link> |
    <router-link to="/vaccine">Vaccine Info </router-link>
  </div>
  <router-view/>
  <div class="footer">
    <p id="lob"> Made with 💚 in Vue </p>
    <div id="site-info">
      <p>All data are APIs are from government sources ,i did't use any third party unofficial APIs
      Vaccination center data are retrived from <a href="https://apisetu.gov.in/public/marketplace/api/cowin/cowin-public-v2#/" id="link">cowin public APIs</a>
      Daily Vaccination Data is retrived from <a href="https://dashboard.cowin.gov.in/" id="link">cowin Portal</a></p>
    </div>
  </div>
</template>

<style>
#app {
  font-family:'Lato', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}
.footer p{
  font-size: 14px;
  line-height: 22px;
}
#site-info{
  padding: 3px;
  width: 350px;
  height: 150px;
}
#lob{
  font-size:16px;
}
.footer{
  display:flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 200px;
  width:100%;
  margin-top:4%;
  background-color: rgba(244, 250, 244 , 0.4);
  color:grey
}

#nav {
  padding: 30px;
  font-size: 13px;
}

#nav a {
  color: #2c3e50;
  text-decoration: none;
  cursor:pointer
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
