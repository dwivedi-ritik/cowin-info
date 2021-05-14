<template>
    <Header />
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
    <Spinner v-else/>
</template>

<script>
import axios from "axios"
import Header from "../components/Header.vue"
import Spinner from "../components/Spinner.vue"

export default {
    name:"Vaccine",
    components:{ Header , Spinner},
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