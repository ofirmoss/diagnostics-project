<template>
  <div class="target_table">
    <div class="column headers">
      <div class="mix regular-column">mix</div>
      <div class="well regular-column">WELL</div>
      <div class="name regular-column">NAME</div>
      <div class="type regular-column">SAMPLE TYPE</div>
      <div class="role regular-column">SAMPLE ROLE</div>
      <div class="results-header">
        <p>RESULT</p>
        <div class="result_row">
          <div class="target result-ind-column ">
            <p>
              TARGET
            </p>
          </div>
          <div class="cls result-ind-column ">
            <p>
              CLASS
            </p>
          </div>
          <div class="ct result-ind-column ">
            <p>CT</p>
          </div>
          <div class="quant result-ind-column ">
            <p>
              QUANT
            </p>
          </div>
          <div class="chart result-ind-column ">
            <p>
              CHART
            </p>
          </div>
        </div>
      </div>
      <div class="messages regular-column">MESSAGES</div>
      <div class="status regular-column">LIMS REPORTING STATUS</div>
      <div class="actions regular-column">ACTIONS</div>
    </div>

    <div class="whole-well" v-for="(row, idx) in getTableAsArray" :key="idx">
      <div class="regular-column mix">
        <p>{{ row.mix_uuid }}</p>
      </div>
      <div class="regular-column well">
        <p>{{ row.name }}</p>
      </div>
      <div class="regular-column name">
        <p>{{ row.patient_id }}</p>
      </div>
      <div class="regular-column type">
        <p>{{ row.specimen_type }}</p>
      </div>
      <div class="regular-column role capitalize">
        <p v-if="row.specimen_tag">{{ row.specimen_tag.replace(/_/g, " ") }}</p>
      </div>
      <div class="results-column ">
        <div
          class="result_row error"
          v-for="(observation_uuid, idx) in row.observation_uuids"
          :key="idx"
        >
          <div class="result-ind-column target">
            <p>{{ data.observations[observation_uuid].mix_channel_uuid }}</p>
          </div>
          <div class="result-ind-column cls">
            <p>{{ data.observations[observation_uuid].classification }}</p>
          </div>
          <div class="result-ind-column ct">
            <p>{{ data.observations[observation_uuid].ct }}</p>
          </div>
          <div class="result-ind-column quant">
            <p>{{ data.observations[observation_uuid].calculated_quantity }}</p>
          </div>
          <div
            class="result-ind-column chart"
            @click.stop="chartClicked(row, data.observations[observation_uuid])"
          >
            <p>
              <trend
                class="trend"
                :data="data.observations[observation_uuid].readings"
                :gradient="['#6fa8dc', '#42b983', '#2c3e50']"
                auto-draw
                smooth
              >
              </trend>
            </p>
          </div>
        </div>
      </div>

      <div class="regular-column messages"><p></p></div>
      <div class="regular-column status capitalize">
        <p v-if="row.lims_status_enum">
          {{ row.lims_status_enum.replace(/_/g, " ") }}
        </p>
      </div>
      <div class="regular-column actions"><p></p></div>
    </div>
  </div>
</template>

<script>
import dataService from "../services/data";
import Vue from "vue";
import Trend from "vuetrend";

Vue.use(Trend);

export default {
  name: "targetTable",
  data() {
    return {
      data: []
    };
  },
  created() {
    this.data = dataService.getData();
    //   console.log(this.getTableAsArray);
  },
  computed: {
    getTableAsArray() {
      let tabaleASArray = [];
      for (const key in this.data.wells) {
        tabaleASArray.push(this.data.wells[key]);
      }
      //   console.log(tabaleASArray);
      return tabaleASArray;
    }
  },
  methods: {
    chartClicked(row, observation) {
      this.$emit("chartClicked", row, observation);
      //   console.log("chartClicked", row,observation)
    }
  }
};
</script>

<style>
.trend {
  cursor: pointer;
}

.capitalize {
  text-transform: capitalize;
}
</style>
