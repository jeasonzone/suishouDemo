<template>
  <div class="wdxy-top">
    <div id="boxArea">
      <canvas id="box" width="550px" height="560px"></canvas>
      <canvas id="fontBox" width="550px" height="560px"></canvas>
    </div>
    <div class="progessBox">
      <Progess :val="val"/>
    </div>
  </div>
</template>

<script>
import Progess from './Progess';
export default {
  name: "HelloWorld",
  components:{
    Progess
  },
  data() {
    return {
      val:977
    };
  },
  mounted() {
    var canvas = document.getElementById("box");
    var ctx = canvas.getContext("2d");

    ctx.translate(275, 330);

    for (var i = 0; i < 19; i++) {
      if (i % 4=== 0) {
        console.log(i);
        ctx.beginPath();
        ctx.lineWidth = "6";
        ctx.strokeStyle = "#ec7259";
        ctx.moveTo(
          137 * Math.sin(((7.5 * i) / 180) * Math.PI),
          -137 * Math.cos(((7.5 * i) / 180) * Math.PI)
        );
        ctx.lineTo(
          155 * Math.sin(((7.5 * i) / 180) * Math.PI),
          -155 * Math.cos(((7.5 * i) / 180) * Math.PI)
        );
        ctx.moveTo(
          -137 * Math.sin(((7.5 * i) / 180) * Math.PI),
          -137 * Math.cos(((7.5 * i) / 180) * Math.PI)
        );
        ctx.lineTo(
          -155 * Math.sin(((7.5 * i) / 180) * Math.PI),
          -155 * Math.cos(((7.5 * i) / 180) * Math.PI)
        );
        ctx.stroke();
        ctx.closePath();
      }
    }
    ctx.font = "";
    ctx.fillStyle = "blue";
    ctx.textAlign = "center";
    var date = new Date();
    var y=date.getFullYear();
    var m=date.getMonth() + 1;
    var d=date.getDate();
    var ymd =
      y + "--" +m + "--" + d;
    ctx.fillText("评估时间 : " + ymd, 0, 95);
    ctx.font = "45px bold";

    var fontBox = document.getElementById("fontBox");
    var ctxPoint = fontBox.getContext("2d");
    function run(inputValue) {
      var timer;
      var i = 0;
      ctxPoint.translate(275, 330);
      ctxPoint.fillStyle = "#7d91f2";
      ctxPoint.strokeStyle = "#7d91f2";

      var finalValue = inputValue;
      var value = 0;

      if (finalValue < 600) {
        value = (finalValue - 357.82) * 0.225;
      } else if (finalValue < 1200) {
        value = (finalValue - 600) * 0.225 + 52.5;
      } else {
         value = finalValue > 1400 ? 1400 : finalValue;
         value = (value - 1200) * 0.27 + 187.5;
      }
      var evalue = " ";
      if (inputValue < 600) {
        evalue = "较差";
      } else if (inputValue < 800) {
        evalue = "中等";
      } else if (inputValue < 1000) {
        evalue = "良好";
      } else if (inputValue < 1200) {
        evalue = "优秀";
      } else {
        evalue = "极好";
      }
      ctxPoint.font = "95px bold";
      ctxPoint.textAlign = "center";
     
      // 所有的动画事件
      function slideValue() {
        ctxPoint.translate(-275, -330);
        ctxPoint.clearRect(0, 0, fontBox.width, fontBox.height);
        ctxPoint.translate(275, 330);
        i++;
        ctxPoint.font = "95px bold";
        var text = 0;
        if (i < 52.5) {
          text = i / 0.225 + 357.8;
        } else if (i < 187.5) {
          text = (i - 52.5) / 0.225 + 600;
        } else {
          text = (i - 187.5) / 0.27 + 1200;
          text = text > 1400 ? 1400 : text;
        }
        text = text > inputValue ? inputValue : text;
        ctxPoint.shadowBlur = 0;
        ctxPoint.fillText(parseInt(text, 10), 0, 35);
        ctxPoint.stroke();
        ctxPoint.font = "20px bold";
        ctxPoint.stroke();
        ctxPoint.closePath();
        // 如果到达所需要的弧度，则停止，否则继续跳动
        if (i > value) {
          setTimeout(function() {
            ctxPoint.fillText("信用" + evalue, 0, 70);
          }, 200);
          clearTimeout(timer);
        } else {
          timer = setTimeout(slideValue, (text / finalValue) * 15);
        }
      }
      slideValue();
    }
    // 打开页面时默认的跳动数字
    run(this.val);
  }
};
</script>
<style scoped>
.progessBox{
  position:absolute;
  top: 77px;
  left: 187px;
}
.wdxy-top {
  position:relative;
  width: 100%;
  height: 500px;
}

.wdxy-top #boxArea {
  position: absolute;
  width: 500px;
  height: 470px;
  margin-top: -70px;
  margin-left: 96px;
}

.wdxy-top #fontBox {
  position: absolute;
  top: 0;
}
</style>