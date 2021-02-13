<template>
  <div class="p-5">
    <div class="w-full flex border-2 border-gray-300 shadow-md mb-10">
      <div class="w-full" v-for="(item, index) in mock" :key="item.message">
        <box :item="item" :index="index"></box>
      </div>
    </div>
    <div v-for="item in receipt" :key="item.no">
      <receipt :item="item"></receipt>
    </div>
    <div
      class="w-full bg-white border-2 border-gray-300 p-6 rounded-md tracking-wide shadow-lg"
    >
      <div id="header" class="flex items-center mb-4">
        <!-- <img
          alt="avatar"
          class="w-20 rounded-full border-2 border-gray-300"
          src="https://picsum.photos/seed/picsum/200"
        /> -->
        <div id="header-text" class="leading-5 ml-6 sm">
          <h4 id="name" class="text-xl font-semibold">REPORT</h4>
          <h5 id="job" class="font-semibold text-blue-600"></h5>
        </div>
      </div>
      <div id="quote" class="flex flex-col">
        <div>Total Parking: {{ totalParking }}</div>
        <div>Total Amount: {{ totalSum }}</div>
      </div>
    </div>
    <!-- <LineChart :chartdata="chart" /> -->
  </div>
</template>
<style>
@import "./output.css";
</style>
<script>
import axios from "axios";
import Box from "./box";
import receipt from "./receipt";
// import LineChart from "./LineChart.vue";
const mock = [
  {
    Parking_lot_ID: 1,
    Parking_lot_status: 0,
    Parking_lot_total_parked: 13,
    Parking_lot_update_time: 1613204234068,
    Total_amount: 220.0,
  },
  {
    Parking_lot_ID: 2,
    Parking_lot_status: 0,
    Parking_lot_total_parked: 1,
    Parking_lot_update_time: 1613204200000,
    Total_amount: 40.0,
  },
  {
    Parking_lot_ID: 3,
    Parking_lot_status: 1,
    Parking_lot_total_parked: 1,
    Parking_lot_update_time: 1613204239068,
    Total_amount: 20.0,
  },
  {
    Parking_lot_ID: 4,
    Parking_lot_status: 0,
    Parking_lot_total_parked: 0,
    Parking_lot_update_time: 0,
    Total_amount: 0,
  },
];
export default {
  components: {
    Box,
    receipt,
  },
  mounted() {
    setInterval(this.fetch, 1000);
    this.report();
    this.chart = {
      labels: ["January", "February", "March", "April", "May", "June", "July"],
      datasets: [
        {
          label: "Data 1",
          data: [2, 10, 5, 9, 0, 6, 20],
          backgroundColor: "transparent",
          borderColor: "rgba(1, 116, 188, 0.50)",
          pointBackgroundColor: "rgba(171, 71, 188, 1)",
        },
      ],
    };
  },
  methods: {
    async fetch() {
      const res = await axios.get("http://exceed2.cpsk-club.xyz/get_all_ava");
      let receipt = {};
      for (let i = 0; i < 4; i++) {
        if (
          res.data.result[i].Parking_lot_status == 0 &&
          this.items.Parking_lot_status == 1
        ) {
          receipt.time = res.data.result[i].Parking_lot_update_time;
          receipt.id = i + 1;
          this.receipt = [...this.receipt, receipt];
        }
      }

      this.items = res.data.result;
    },
    report() {
      let totalParking = 0;
      let totalSum = 0;
      mock.map((item) => {
        totalParking += item.Parking_lot_total_parked;
        totalSum += item.Total_amount;
      });
      this.totalParking = totalParking;
      this.totalSum = totalSum;
    },
  },
  data() {
    return {
      chart: {},
      receipt: [],
      totalParking: 0,
      totalSum: 0,
      items: [
        { Parking_lot_ID: "Foo", Parking_lot_status: 1, Total_amount: "10" },
        { message: "Bar" },
      ],
      mock,
    };
  },
};
</script>
