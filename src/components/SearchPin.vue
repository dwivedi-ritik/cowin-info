<template>
    <div class="form-inp" >
        <form @submit.prevent="fetchResult">
            <div class=usr-inp>
                <label >Pincode </label>
                <input type="text" class="inp-pin" v-model="pincode" required>
            </div>
            <div class=usr-inp>
                <label>Date </label>
                <input type="text" class="inp-date" v-model="date" required>
            </div>
            <input type="submit" value="Find Centers" class="submit-btn" > 
        </form>
    </div>
</template>

<script>
import axios from "axios"

export default {
    name:"SearchPin",
    data(){
        return{
            pincode:null,
            date:null,
            url:"https://cdn-api.co-vin.in/api/v2/appointment/sessions/public/calendarByPin",
            allResults:[]
        }
    },
    methods:{
        async fetchResult(){
            try{
            let res = await axios({
                method:"get",
                url:this.url,
                params:{
                    pincode:this.pincode,
                    date:this.date
                }
            })
            this.allResults = await res.data["centers"]
            }
            catch(err){
                this.allResults = []
            }
            this.$emit("recieveData" , this.allResults)
        }
    }

}
</script>

<style>
*{
    padding: 0%;
    margin: 0%;
}
.form-inp {
    margin-top: 80px;
    width: 100vw;
    height: 150px;
}
.inp-pin , .inp-date{
    min-width:180px;
    width: 220px;
    min-height: 20px;
    height: 20px;
    padding:6px;
    border-radius: 5px;
    border:blueviolet 2px solid;
    color: blueviolet;
    opacity: 0.9;
}
.inp-pin , .inp-date:focus{
    outline: none;
    opacity: 1;
}
.usr-inp{
    position: relative;
}
form{
    height: 130px;
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    align-items: center;
}
.form-inp label{
    position: absolute;
    z-index: 1;
    top: 0%;
    left: 4%;
    top: -18%;
    font-size: 10px;
    font-weight: 600;
    background-color: white;
    color: blueviolet;
    padding: 2px;
}
.submit-btn{
    width: 100px;
    height: 30px;
    background-color: blueviolet;
    color: white;
    border-radius: 3px;
    border: none;
    padding: 4px;
    opacity: 0.9;
}
.submit-btn:hover{
    cursor: pointer;
    opacity: 1;
}
.submit-btn:focus{
    outline: none;
}

.show-data{
    width: 100vw;
    height: auto;
    display: flex;
    flex-direction: column;
    justify-content:space-evenly;
    align-items: center;
}

</style>