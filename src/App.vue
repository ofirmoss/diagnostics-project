<template>
  <div id="app" @click="closeModal">
    <target-table @chartClicked="updateCurrentChart"></target-table>
    <modal :modalContent="modalContent" :showModal="showModal"></modal>
  </div>
</template>

<script>
import targetTable from "./components/target_table";
import modal from "./components/modal";

export default {
  name: "app",
  components: {
    targetTable,
    modal
  },
  data() {
    return {
      modalContent: {},
      showModal: false
    };
  },
  methods: {
    updateCurrentChart(row, observation) {
      this.modalContent = {
        well_name: row.well_name,
        mix_channel_uuid: observation.mix_channel_uuid,
        readings: observation.readings
      };
      this.showModal = true;
      // console.log(this.modalChart,this.showModal )
    },
    closeModal() {
      this.showModal = false;
      // console.log('modal closed')
    }
  }
};
</script>

<style>
#app {
  position: relative;
}

body {
  font-family: Helvetica, Arial, sans-serif;
  font-size: 14px;
}

div {
  padding: 1%;
  overflow: hidden;
  word-break: normal;
}

p {
  padding: 0;
  margin: 0;
}

.target_table {
  display: table;
}

.headers {
  font-weight: bold;
  color: #064b64;
  padding: 1%;
  background-color: white;
  word-break: normal;
  text-transform: uppercase;
  display: table-row;
}
.regular-column,
.results-columns,
.result-ind-column {
  display: table-cell;
  text-align: center;
  vertical-align: top;
}
.results-header {
  display: block;
  padding: 0;
  text-align: center;
}
div .mix {
  width: 5%;
  text-transform: uppercase;
  vertical-align: middle;
}
div .well {
  width: 4%;
  vertical-align: middle;
}
div .name {
  width: 7%;
  vertical-align: middle;
}
div .type {
  width: 8%;
  vertical-align: middle;
}
div .role {
  width: 7%;
  vertical-align: middle;
}
div .messages {
  width: 12%;
  vertical-align: middle;
}
div .status {
  width: 12%;
  vertical-align: middle;
}
div .actions {
  width: 4%;
  vertical-align: middle;
}

.whole-well {
  background: white;
  display: table-row;
  width: 98%;
  padding: 1%;
}
.whole-well:nth-child(even) {
  background: #e0e0e0;
}
.error {
  background: #ffdb87;
}

.result_row {
  display: block;
}

div .target {
  width: 20%;
  display: inline-block;
}
div .cls {
  width: 14%;
  display: inline-block;
}
div .ct {
  width: 12%;
  display: inline-block;
}
div .quant {
  width: 14%;
  display: inline-block;
}
div .chart {
  width: 25%;
  display: inline-block;
}

.modal {
  border: #2da8cb solid;
  width: 66vw;
  height: 66vh;
  background: white;
  padding: 0;
  position: absolute;
  top: 50px;
  left: 19vw;
}

.modal-header {
  background: #2da8cb;
  vertical-align: middle;
  color: white;
}

.curve {
  height: 40vh;
  background: #1d6b82;
  color: white;
}

.lightbox_table {
}

.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: table;
  transition: opacity 0.3s ease;
}

.modal-wrapper {
  display: table-cell;
  vertical-align: middle;
}

.modal-container {
  width: 300px;
  margin: 0px auto;
  padding: 20px 30px;
  background-color: #fff;
  border-radius: 2px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
  transition: all 0.3s ease;
  font-family: Helvetica, Arial, sans-serif;
}

.modal-header h3 {
  margin-top: 0;
  color: #42b983;
}

.modal-body {
  margin: 20px 0;
}

.modal-default-button {
  float: right;
}

/*
  * The following styles are auto-applied to elements with
  * transition="modal" when their visibility is toggled
  * by Vue.js.
  *
  * You can easily play with the modal transition by editing
  * these styles.
  */

.modal-enter {
  opacity: 0;
}

.modal-leave-active {
  opacity: 0;
}

.modal-enter .modal-container,
.modal-leave-active .modal-container {
  -webkit-transform: scale(1.1);
  transform: scale(1.1);
}

.error {
  background-color: #ffa07a;
}
</style>
