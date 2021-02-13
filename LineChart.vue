<script>
import { Line, mixins } from "vue-chartjs";
const { reactiveProp } = mixins;
export default {
  extends: Line,
  // mounted() {
  //   this.renderChart(
  //     {
  //       labels: [
  //         "January",
  //         "February",
  //         "March",
  //         "April",
  //         "May",
  //         "June",
  //         "July",
  //       ],
  //       datasets: [
  //         {
  //           label: "Data 1",
  //           data: [2, 10, 5, 9, 0, 6, 20],
  //           backgroundColor: "transparent",
  //           borderColor: "rgba(1, 116, 188, 0.50)",
  //           pointBackgroundColor: "rgba(171, 71, 188, 1)",
  //         },
  //       ],
  //     },
  //     {
  //       responsive: true,
  //       maintainAspectRatio: false,
  //       title: {
  //         display: true,
  //         text: "My Data",
  //       },
  //     }
  //   );
  // },  extends: Line,
  mixins: [reactiveProp],
  props: ["options"],
  mounted() {
    // this.chartData is created in the mixin.
    // If you want to pass options please create a local options object
    this.renderChart(this.chartData, this.options);
  },
};
</script>
