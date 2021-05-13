<template>
  <div class="home">
    <span class="title-info">Vaccination center info</span>
    <p class="title-detail">This site usases <a href="https://apisetu.gov.in/public/marketplace/api/cowin/cowin-public-v2#/" id="link"> Cowin public APIs</a> for fetching data.
    <br>Enter your area pincode with date</p>
    <img src ="../../assets/img.png" width="50" id="img-logo">  
  </div>
    <SearchPin @recieveData="shower"></SearchPin>
    <ShowData v-if="showResult" :allData=allData ></ShowData>
    <p style="text-align=center; color:red; font-size:12px;" v-if="noRecords"> No records found</p>
</template>

<script>
import SearchPin from '../components/SearchPin.vue'
import ShowData from '../components/ShowData'

export default {
  name: 'Home',
  components: { ShowData , SearchPin },
  data(){
    return {
      showResult:false,
      allData:[],
      noRecords:false
    }
  },
  methods:{
    shower(res){
      this.allData = res
      if(!this.allData.length){
        this.showResult = false
        this.noRecords = true
      }else{
        this.showResult = true
        this.noRecords = false
      }
    }
  }
}
</script>
<style scoped>
header{
  width: 100vw;
  height: 100px;
  display: flex;
  align-items: center;
  justify-content: center;
}
#img-logo{
  padding-top:3%;
}
#link{
  color:blueviolet;
  text-decoration: none;
}
.title-detail{
  margin-top:20px;
  font-size: 12px;
  line-height: 20px;
}
.title-info{
  font-family: sans-serif;
  font-size: 20px;
  font-weight: 600;
  text-align: center;
}
</style>
