<template>
    <div class="state-select">
        <select @change="stateVacData" v-model="selectedState" id="op-selec">
            <option> Select State </option>
            <option v-for="( state , index) in states" :key=index>{{ state }}</option>
        </select>
    </div>
</template>
<script>
import { allStates , getDate , URL} from "./state.js"
import axios from "axios"
export default {
    name:"StateSelection",
    emits:["getStateData"],
    data(){
        return {
            states :allStates,
            selectedState:null,
            retrivedStateData:null
        }
    },
    methods:{
        async stateVacData(){
            let stateCode = allStates.indexOf(this.selectedState) + 1
            try {
                let res = await axios({
                    method:"get",
                    url:URL,
                    params:{"state_id":stateCode , "date":getDate() } })
                this.retrivedStateData = ( await res.data ).topBlock
            } catch (error) {
                this.retrivedStateData = null
            }
            this.$emit("getStateData" , this.retrivedStateData)    
        }
    }
}
</script>

<style>
.state-select{
    margin-top:2%;
    width: 100vw;
    height: 30px;
    display: flex;
    justify-content: space-evenly;
    align-items: center;
}

#op-selec {
    padding: 5px;
}
#op-selec:focus {
    outline: none;
}
@media only screen and (max-width: 840px) {
    .state-select {
        margin-top: 4%;
    }
}
</style>