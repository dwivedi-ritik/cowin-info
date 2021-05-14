<template>
    <div class="head-info">
        <p>Daily Vaccination Information</p><br>
        <div class="head-detail-in">
            <p id="head-text">Source of data is <a href="https://dashboard.cowin.gov.in/" id="link">Cowin-portal </a>, 
                click at Cowin text for more information
                wll i know site is incomplete in many , i made it just as pratice project 
                details at the side of arrow shows the todays increased data </p>
        </div>
    </div>
    <div class="parent-vac-info" v-if="showData">
        <div class="vac-info">
            <p id="title-text">Each Doses Count</p>
            <div id="daily-info">
                <p>First Dose {{ vaccineData.vaccination.tot_dose_1.toLocaleString() }}</p>
                <span class="material-icons tred-icon">
                    trending_flat
                </span>
            </div>
            <div id="daily-info">
                <p>Second Dose {{ vaccineData.vaccination.tot_dose_2.toLocaleString() }}</p>
                <span class="material-icons tred-icon">
                    trending_flat
                </span>
            </div>
            <span class="material-icons ana-icon">
                analytics
            </span>
        </div>
        <div class="vac-info">
            <p id="title-text">Fully Vaccined</p>
            <p>{{ vaccineData.vaccination.total_doses.toLocaleString()}}</p>
            <div id="daily-info">
                <p style="color:green;">{{ vaccineData.vaccination.today.toLocaleString() }}</p>
                <span class="material-icons tred-icon">
                    trending_flat
                </span>
            </div>
            <span class="material-icons ana-icon">
                analytics
            </span>
        </div>
        <div class="vac-info">
            <p id="title-text">Total Doses</p>
            <p> Covaxin  {{ vaccineData.vaccination.covaxin.toLocaleString()}}</p>
            <p> Covishield {{ vaccineData.vaccination.covishield.toLocaleString()}}</p>
            <span class="material-icons ana-icon" c>
                analytics
            </span> 
        </div>
    </div>
    <div class="spinner" v-else>
        <div class="spin-center">
            <div class="spin"></div>
        </div>
    </div>
</template>

<script>
import axios from "axios"


export default {
    name:"Vaccine",
    data(){
        return {
            url:"https://api.cowin.gov.in/api/v1/reports/v2/getPublicReports",
            vaccineData:null,
            showData:false
        }
    },
    methods:{
        getDate(){
            let date = new Date()
            let month = parseInt(date.getMonth())+1
            return date.getFullYear()+"-"+month+"-"+date.getDate()
        },
        async getVaccineData(){
            let res = await axios({
                url:this.url,
                method:"get",
                params:{
                    date:this.getDate()
                }
            })
            this.vaccineData = (await res.data).topBlock       
        }
    },
    mounted(){
        this.getVaccineData()
        .then(()=>{this.showData = true})
    }
}
</script>

<style>

.spinner{
    width: 100vw;
    height: 200px;
    display: flex;
    align-items: center;
    justify-content: center;
}
.spin{
    display: block;
    width:40px;
    height: 40px;
    border:3px solid transparent;
    border-radius: 50%;
    border-top-color: blueviolet;
    animation: spin 1s ease-in infinite;
}
@keyframes spin {
    to { transform: rotateZ(360deg) }
}
#head-text{
    color: dimgrey;
    font-size:14px;
    line-height: 18px;
}
.head-info{
    margin-top: 3%;
    width: 100vw;
    height: 100px;
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    align-items: center;
}
.head-detail-in{
    height: 180px;
    width: 450px;
}
#daily-info {
    display: flex;
    justify-content: center;
    align-items: center;
}
.parent-vac-info{
    margin-top:4%;
    width:100vw;
    height:300px;
    display: flex;
    justify-content:space-around;
    align-items: center;
    background-color: #f4f6f9;
}

.vac-info{
    font-size: 15px;
    color: dimgrey;
    display:flex;
    flex-direction: column;
    justify-content: space-around;
    position: relative;;
    width: 280px;
    min-width: 220px;
    height: 150px;
    padding:8px;
    background-color: #fff;
    border-radius: 4px;
    box-shadow: 2px 3px 3px rgba(0,0,0,0.1);
}
.vac-info:hover{
    box-shadow: 2px 3px 3px rgba(0,0,0,0.2);
    cursor: pointer;

}
.ana-icon{
    position:absolute;
    right: 4%;
    bottom: 4%;
}
.tred-icon{
    font-size: 20px;
    font-weight: bolder;
    transform: rotate(-90deg);
}
.material-icons{
    color:rgba(0,0,0,0.2);
}
@media only screen and (max-width: 840px) {
    .parent-vac-info{
        flex-direction: column;
        justify-content: space-evenly;
        height: 500px;
    }
    .vac-info{
        padding:0;
    }
    .head-detail-in{
        width: 350px;
    }
}
</style>