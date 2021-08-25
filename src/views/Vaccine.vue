<template>
  <Header />
  <StateSelection @getStateData="gettingStateData" />
  <div class="parent-vac-info" v-if="showData">
    <div class="vac-info">
      <p id="title-text">Dose Count</p>
      <div id="daily-info">
        <p>
          First-Dose
          <span id="nm-d">{{
            vaccineData.vaccination.tot_dose_1.toLocaleString()
          }}</span>
        </p>
      </div>
      <div id="daily-info">
        <p>
          Second-Dose
          <span id="nm-d">{{
            vaccineData.vaccination.tot_dose_2.toLocaleString()
          }}</span>
        </p>
      </div>
      <span class="material-icons ana-icon"> analytics </span>
    </div>
    <div class="vac-info">
      <p id="title-text">Fully Vaccined</p>
      <p>{{ vaccineData.vaccination.total_doses.toLocaleString() }}</p>
      <div id="daily-info">
        <p style="color: green">
          Today {{ vaccineData.vaccination.today.toLocaleString() }}
        </p>
        <span class="material-icons tred-icon"> trending_flat </span>
      </div>
      <span class="material-icons ana-icon"> analytics </span>
    </div>
    <div class="vac-info">
      <p id="title-text">Vaccine Type</p>
      <p>Covaxin {{ vaccineData.vaccination.covaxin.toLocaleString() }}</p>
      <p>
        Covishield {{ vaccineData.vaccination.covishield.toLocaleString() }}
      </p>
      <span class="material-icons ana-icon" c> analytics </span>
    </div>
  </div>
  <Spinner v-else />
</template>

<script>
import axios from "axios";
import Header from "../components/Header.vue";
import Spinner from "../components/Spinner.vue";
import StateSelection from "../components/StateSelection.vue";
import { getDate, URL } from "../components/state.js";

export default {
  name: "Vaccine",
  components: { Header, Spinner, StateSelection },
  data() {
    return {
      vaccineData: null,
      showData: false,
    };
  },
  methods: {
    async getVaccineData() {
      let res = await axios({
        url: URL,
        method: "get",
        params: {
          date: getDate(),
        },
      });
      this.vaccineData = (await res.data).topBlock;
    },
    gettingStateData(stateData) {
      if (!stateData) {
        this.getVaccineData();
      } else {
        this.vaccineData = stateData;
      }
    },
  },
  mounted() {
    this.getVaccineData().then(() => {
      this.showData = true;
    });
  },
};
</script>

<style>
#daily-info {
  display: flex;
  justify-content: center;
  align-items: center;
}

.parent-vac-info {
  margin: 4% auto;
  width: 60%;
  display: flex;
  justify-content: space-around;
  align-items: center;
}

.vac-info {
  font-size: 15px;
  color: dimgrey;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  min-width: 250px;
  height: 150px;
  padding: 8px;
  background-color: #fff;
  border-radius: 4px;
  box-shadow: 2px 3px 3px rgba(0, 0, 0, 0.1);
}
.vac-info:hover {
  box-shadow: 2px 3px 3px rgba(0, 0, 0, 0.2);
  cursor: pointer;
}
.ana-icon {
  position: absolute;
  right: 4%;
  bottom: 4%;
}
.tred-icon {
  font-size: 20px;
  font-weight: bolder;
  transform: rotate(-90deg);
  color: rgba(0, 0, 0, 0.2);
}
@media only screen and (max-width: 840px) {
  .parent-vac-info {
    flex-direction: column;
    justify-content: space-evenly;
    height: 500px;
  }
  .vac-info {
    padding: 0;
  }
  .head-detail-in {
    width: 350px;
  }
}
</style>