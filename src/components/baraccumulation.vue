<template>
  <div class='vue_charts'>
    <div class='box'>
      <div class="titleleft">样式扩展</div>
      <div id="main"></div>
      <div class="application">
        <p>应用场景:年/月度数目或占比情况,分类占比等</p>
        <p>展示效果:如上图所示</p>
        <p>功能描述:柱状图表示，方便用户展示引用</p>
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
      var xAxisData = []
      var data1 = []
      var data2 = []
      var data3 = []
      var data4 = []
      for (var i = 0; i < 10; i++) {
        xAxisData.push('Class' + i)
        data1.push((Math.random() * 2).toFixed(2))
        data2.push(-Math.random().toFixed(2))
        data3.push((Math.random() * 5).toFixed(2))
        data4.push((Math.random() + 0.3).toFixed(2))
      }
      var itemStyle = {
        normal: {
        },
        emphasis: {
          barBorderWidth: 1,
          shadowBlur: 10,
          shadowOffsetX: 0,
          shadowOffsetY: 0,
          shadowColor: 'rgba(0,0,0,0.5)'
        }
      }
      myChart.setOption({
        backgroundColor: '#eee',
        legend: {
          data: ['bar', 'bar2', 'bar3', 'bar4'],
          align: 'left',
          left: 10
        },
        brush: {
          toolbox: ['rect', 'polygon', 'lineX', 'lineY', 'keep', 'clear'],
          xAxisIndex: 0
        },
        toolbox: {
          feature: {
            magicType: {
              type: ['stack', 'tiled']
            },
            dataView: {}
          }
        },
        tooltip: {},
        xAxis: {
          data: xAxisData,
          name: 'X Axis',
          silent: false,
          axisLine: {onZero: true},
          splitLine: {show: false},
          splitArea: {show: false}
        },
        yAxis: {
          inverse: true,
          splitArea: {show: false}
        },
        grid: {
          left: 100
        },
        visualMap: {
          type: 'continuous',
          dimension: 1,
          text: ['High', 'Low'],
          inverse: true,
          itemHeight: 200,
          calculable: true,
          min: -2,
          max: 6,
          top: 60,
          left: 10,
          inRange: {
            colorLightness: [0.4, 0.8]
          },
          outOfRange: {
            color: '#bbb'
          },
          controller: {
            inRange: {
              color: '#2f4554'
            }
          }
        },
        series: [
          {
            name: 'bar',
            type: 'bar',
            stack: 'one',
            itemStyle: itemStyle,
            data: data1
          },
          {
            name: 'bar2',
            type: 'bar',
            stack: 'one',
            itemStyle: itemStyle,
            data: data2
          },
          {
            name: 'bar3',
            type: 'bar',
            stack: 'two',
            itemStyle: itemStyle,
            data: data3
          },
          {
            name: 'bar4',
            type: 'bar',
            stack: 'two',
            itemStyle: itemStyle,
            data: data4
          }
        ]
      })
      window.onresize = myChart.resize
    }
  }
}
</script>

<!-- Add 'scoped' attribute to limit CSS to this component only -->
<style scoped>
.box {
  position: absolute;
  bottom: 0;
  top: 0;
  right: 0;
  left: 0;
  background: #f2f2f2;
  border-top: 1px solid #bbbebd;
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
