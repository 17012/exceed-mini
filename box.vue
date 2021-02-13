<template>
  <div class="w-full flex flex-col items-center justify-center">
    <div
      v-if="item.Parking_lot_status"
      class="w-full bg-green-200 box-h text-center p-5"
    >
      <div>No.</div>
      <div>{{ item.Parking_lot_ID }}</div>
      <div>Time</div>
      <div>{{ time }}</div>
    </div>
    <div v-else class="w-full bg-red-200 box-h text-center p-5">
      <div>No.</div>
      <div>{{ item.Parking_lot_ID }}</div>
      <div>Available</div>
    </div>
    <div class="mt-2 flex-1">
      Total Parked: {{ item.Parking_lot_total_parked }}
    </div>
    <div class="mt-2 flex-1"></div>
  </div>
</template>
<style>
@import "./output.css";

.box-h {
  min-height: 300px;
}
</style>
<script>
export default {
  props: {
    item: {},
  },
  data() {
    return {
      time: "0s",
    };
  },
  mounted() {
    setInterval(() => {
      const time = (Date.now() - this.item.Parking_lot_update_time) / 1000;
      if (this.item.Parking_lot_update_time === 0) return "0s";
      let str = "";
      if (Math.floor(time / 3600) > 0) str += Math.floor(time / 3600) + " h ";
      if (Math.floor((time / 60) % 60) > 0)
        str += Math.floor((time / 60) % 60) + " m ";
      str += Math.floor(time % 60) + " s";
      this.time = str;
    }, 1000);
  },
};
</script>
