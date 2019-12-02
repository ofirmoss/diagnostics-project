<template>
  <div class="modal" v-if="showModal" @click.stop="">
    <div class="modal-header">
      <p>
        {{ modalContent.well_name }}
      </p>
    </div>
    <div class="curve">
      <highcharts :options="modalContent.readings"></highcharts>
    </div>
    <div class="lightbox_table">
      <p>Target is: {{ modalContent.mix_channel_uuid }}</p>
    </div>
  </div>
</template>

<script>
import { Chart } from "highcharts-vue";

export default {
  name: "modal",
  props: ["showModal", "modalContent"],
  watch: {
    showModal: function() {
      console.log(this.showModal, this.modalContent);
    }
  },
  components: {
    highcharts: Chart
  }
};
</script>

<style>
.curve {
    /* width: 100%;
    height: 200px; */
}
</style>
