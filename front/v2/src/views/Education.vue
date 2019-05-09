<template>
  <div class="container">
    <h2 class="text-center">学历和薪资分析图</h2>
        <ve-pie :title="chartTitle" :data="chartData"></ve-pie>
        <ve-histogram :title="salartTitle" :data="salaryData" :settings="salarySettings"></ve-histogram>
    
  </div>
</template>

<script>
import { get_education } from "@/service/api";
import VeHistogram from "v-charts/lib/histogram.common";
import VePie from "v-charts/lib/pie.common";
import "echarts/lib/component/title";
export default {
  components: { VeHistogram, VePie },
  data() {
    this.chartTitle = {
      text: "招聘中学历分析"
    };
    this.salartTitle ={
        text: "学历和薪资分析"
    }
    return {
      salarySettings: {
        labelMap: {
          educational: "学历",
          salary: "平均薪资"
        },
        digit: 0,
        xAxisType: "category"
      },
      chartData: {
        columns: ["educational", "count"],
        rows: []
      },
      salaryData: {
        columns: ["educational", "salary"],
        rows: []
      }
    };
  },
  mounted() {},
  async created() {
    // let responseData = await get_education();
    let responseData = [{"count":28,"salary":12214.285714285714,"educational":"\u5b66\u5386\u4e0d\u9650"},{"count":305,"salary":13704.918032786885,"educational":"\u4e0d\u9650"},{"count":1285,"salary":14615.175097276264,"educational":"\u5927\u4e13"},{"count":2412,"salary":17860.074626865673,"educational":"\u672c\u79d1"},{"count":11,"salary":20500,"educational":"\u7855\u58eb"}];
    this.chartData.rows = this.salaryData.rows = responseData;
  },
  methods: {}
};
</script>