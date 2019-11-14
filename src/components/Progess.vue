<template>
  <div>
    <el-progress
      type="dashboard"
      :width="368"
      :height="386"
      :percentage="percentage"
      :color="colors"
      :show-text=false
      class="progress"
    ></el-progress>
  </div>
</template>

<script>
import { log } from 'util';
export default {
  name: "Progess",
  props: {
    val: {
      type: Number,
      default: '0'
    }
  },
  mounted() {
    var result=(this.val/1400)*100;
    this.percentage = 0;
    setTimeout(() => {
      this.percentage = result;
    }, 1000);
  },
  data() {
    return {
      percentage: 0,
      colors: [
        { color: "rgb(245, 8, 8)", percentage: 20 },
        { color: "rgb(226, 161, 117)", percentage: 40 },
        { color: "rgb(199, 216, 46)", percentage: 60 },
        { color: "rgb(46, 240, 207)", percentage: 80 },
        { color: "rgb(36, 250, 8)", percentage: 100 }
      ]
    };
  }
};
</script>
<style scoped>
</style>