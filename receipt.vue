<template>
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
        <h4 id="name" class="text-xl font-semibold">
          No.{{ item.id }} Summary
        </h4>
      </div>
    </div>
    <div id="quote" class="flex flex-col">
      <div>Time parking: {{ parkingTime }}</div>
      <div>Total Amount: {{ totalSum }}</div>
    </div>
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
      sum: 0,
    };
  },
  mounted() {
    const time = (Date.now() - this.item.time) / 1000;
    if (this.item.time === 0) return "0s";
    let str = "";
    if (Math.floor(time / 3600) > 0) str += Math.floor(time / 3600) + " h ";
    if (Math.floor((time / 60) % 60) > 0)
      str += Math.floor((time / 60) % 60) + " m ";
    str += Math.floor(time % 60) + " s";
    this.time = str;
    this.sum = Math.ceil(time / 60) * 20;
  },
};
</script>
