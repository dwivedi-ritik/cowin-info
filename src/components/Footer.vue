<template>
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
.footer p{
  font-size: 14px;
  line-height: 22px;
}
#site-info{
  padding: 3px;
  width: 350px;
}
#lob{
  font-size:16px;
}
.footer{
  margin-top:4%;
  display:flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
  width:100vw;
  height:180px;
  background-color: rgba(244, 250, 244 , 0.4);
  /* background-color: blueviolet  ; */
  color:grey

}

</style>