<template>
    <div class="usr-choice">
        <div class="title"> <p> Select Vaccination Center</p></div>
        <select  v-model="selected" @change="changedOption" class="opt">
            <option v-for="centerData in allData" :key="centerData.name" >{{ centerData.name }}</option>
        </select>
    </div>
    <div class="details">
        <div class="result" v-if="showCenter">
            <p>{{ result.name }}</p>
            <p style="color:green;">Availablity {{ result.sessions[0].date }}</p>
            <div class="info"> {{ result.sessions[0].vaccine }} ({{ result.sessions[0].min_age_limit }}+) - {{ result.sessions[0].available_capacity }}</div>
        </div>
    </div>
</template>

<script>
export default {
    name:"ShowData",
    props:["allData"],
    data(){
        return {
            selected:"",
            showCenter:false,
            result :null,
        }
    },
    methods:{
        changedOption(){
            for(let obj of this.allData){
                if(obj.name == this.selected){
                    this.result = obj
                    this.showCenter = true
                    break
                }
            }
        }
    }
}


</script>

<style>
.opt{
    padding: 3px;
    font-size: 11px;
    border-left: 3px blueviolet solid;
    width: auto;
    min-width: 100px;
    cursor: pointer;
}
.opt:focus{
    outline: none;
}
.usr-choice{
    height: 100px;
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    align-items: center;
}
.title{
    display: block;
    font-size: 12px;
    border-left: 3px blueviolet solid;
    width: 180px;
    height: 30px;
    padding: 2px;
    background-color: rgba(138, 43, 226 , 0.2);

}
.title p{
    text-align: center;
    vertical-align: middle;
    line-height: 30px;

}
.details{
    width: 100vw;
    height: 200px;
    display: flex;
    justify-content: center;
    align-items: center;
}
.result{
    width: 200px;
    height: 80px;
    max-height: auto;
    border-top-left-radius: 2px;
    border-bottom-left-radius: 2px; 
    border:2px rgba(0, 0, 0, 0.2) solid;
    font-size: 11px;
    font-weight: 600;
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;
    align-items: center;
}
.info{
    padding: 3px;
    background-color:rgba(84, 169, 0, 0.7);
    color: white;
    border-radius: 2px;
    width: auto;
}
</style>