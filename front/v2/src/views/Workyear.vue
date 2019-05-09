<template lang="">
    <div class="container">
        <h2 class="text-center">工作年限和薪资分析</h2>
         <ve-pie :data="chartData" :settings="pieSettings" :colors="colors"></ve-pie>
         <ve-histogram :data="salaryData"  :settings="salarySettings"></ve-histogram>
    </div>
    
</template>

<style scoped>
</style>

<script>
import VePie from "v-charts/lib/pie.common";
import VeHistogram from "v-charts/lib/histogram.common";
import { get_work_year } from "@/service/api";
export default {
  components: { VePie, VeHistogram },
  data() {
    return {
      colors: [
        "#c23531",
        "#2f4554",
        "#61a0a8",
        "#d48265",
        "#91c7ae",
        "#749f83",
        "#ca8622",
        "#bda29a",
        "#6e7074",
        "#546570",
        "#c4ccd3"
      ],
      pieSettings: {
        labelMap: {
          work_year: "类型",
          count: "发布数"
        },
        yAxisType: ["normal"],
        dataType: function(v) {
          return v + "个";
        }
      },
      chartData: {
        columns: ["work_year", "count"],
        rows: []
      },
      salarySettings: {
        labelMap: {
          work_year: "工作年限",
          salary: "平均薪资"
        },
        digit: 0,
        xAxisType: "category"
      },
      salaryData: {
        columns: ["work_year", "salary"],
        rows: []
      }
    };
  },
  async created() {
    // let response = await get_work_year();
    let response = [{"count":67,"salary":6574.626865671642,"work_year":"\u5e94\u5c4a\u751f"},{"count":145,"salary":11437.931034482759,"work_year":"1\u5e74\u4ee5\u5185"},{"count":1229,"salary":12153.783563873067,"work_year":"1-3\u5e74"},{"count":198,"salary":13669.191919191919,"work_year":"\u7ecf\u9a8c\u4e0d\u9650"},{"count":1857,"salary":17946.149703823372,"work_year":"3-5\u5e74"},{"count":540,"salary":24825.925925925927,"work_year":"5-10\u5e74"},{"count":5,"salary":26400,"work_year":"10\u5e74\u4ee5\u4e0a"}];
    this.chartData.rows = response;
    this.salaryData.rows = response;
  }
};
</script>