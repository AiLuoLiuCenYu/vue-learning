<template>
  <div class="vue_charts">
    <div class="box">
      <div class="titleleft">折线图样式扩展</div>
      <div id="main"></div>
      <div class="application">
        <p>应用场景:年/月/日度数目情况等</p>
        <p>展示效果:如上图所示</p>
        <p>功能描述:极坐标表示，方便用户展示引用/比较</p>
        <p>开发简单描述:使用china.js展示柱状图，引入多个数据，使用echarts.js修正样式及功能</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'rightbox',
  data () {
    return {
      isCollapse: false
    }
  },
  mounted () {
    this.drawLine()
  },
  methods: {
    drawLine () {
      let myChart = this.$echarts.init(document.getElementById('main'))
      // 绘制图表
      var data = []
      for (var i = 0; i <= 360; i++) {
        var t = i / 180 * Math.PI
        var r = Math.sin(2 * t) * Math.cos(2 * t)
        data.push([r, i])
      }
      myChart.setOption({
        title: {
          text: '极坐标双数值轴'
        },
        legend: {
          data: ['line']
        },
        polar: {
          center: ['50%', '54%']
        },
        tooltip: {
          trigger: 'axis',
          axisPointer: {
            type: 'cross'
          }
        },
        angleAxis: {
          type: 'value',
          startAngle: 0
        },
        radiusAxis: {
          min: 0
        },
        series: [{
          coordinateSystem: 'polar',
          name: 'line',
          type: 'line',
          showSymbol: false,
          data: data
        }],
        animationDuration: 2000
      })
      window.onresize = myChart.resize
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.box {
  position: absolute;
  bottom: 0;
  top: 0;
  right: 0;
  left: 0;
  background: #f2f2f2;
  border-top:1px solid #bbbebd;
}
#main {
  margin: 3% auto;
  width:90%;
  height:53%;
}
.application{
  height:28%;
  padding:0 5%;
}
.application>p{
  font-size:14px;
  color:#a1a5a4;
  font-family: "微软雅黑";
}
.titleleft{
  text-align:center;
  margin-top:20px;
  font-size:14px;
  color:#4e4e4e;
}
</style>
