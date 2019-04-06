<template>
  <el-row :gutter="0">
    <!-- 为 ECharts 准备一个具备大小（宽高）的 DOM -->
    <el-col id="eg1" :xs="24" :sm="24" :lg="12" style="height:400px;"></el-col>
    <el-col id="eg2" :xs="24" :sm="24" :lg="12" style="height:400px;"></el-col>
    <el-col :sm="24">
      <HelloWorld2/>
    </el-col>
  </el-row>
</template>

<script>
  import HelloWorld2 from "@/components/HelloWorld2";
  export default {
    name: 'HelloWorld',
    components: {HelloWorld2},
    data() {
      return {
        eg1Options: {
          title: {
            text: 'ECharts 入门示例'
          },
          tooltip: {},
          legend: {
            data: ['销量']
          },
          xAxis: {
            data: ["衬衫", "羊毛衫", "雪纺衫", "裤子", "高跟鞋", "袜子"]
          },
          yAxis: {},
          series: [{
            name: '销量',
            type: 'bar',
            data: [5, 20, 36, 10, 10, 20]
          }]
        }
      }
    },
    methods: {
      bindEg1() {
        // 基于准备好的dom，初始化echarts实例
        var myChart = this.$echarts.init(document.getElementById('eg1'));

        // 指定图表的配置项和数据
        // 使用刚指定的配置项和数据显示图表。
        myChart.setOption(this.eg1Options);

        window.addEventListener('resize', () => myChart.resize());
      },
      bindEg2() {
        // 基于准备好的dom，初始化echarts实例
        var myChart = this.$echarts.init(document.getElementById('eg2'));

        var base = +new Date(2014, 9, 3);
        var oneDay = 24 * 3600 * 1000;
        var date = [];

        var data = [Math.random() * 150];
        var now = new Date(base);

        function addData(shift) {
          now = [now.getFullYear(), now.getMonth() + 1, now.getDate()].join('/');
          date.push(now);
          data.push((Math.random() - 0.4) * 10 + data[data.length - 1]);

          if (shift) {
            date.shift();
            data.shift();
          }

          now = new Date(+new Date(now) + oneDay);
        }

        for (var i = 1; i < 100; i++) {
          addData();
        }

        let option = {
          xAxis: {
            type: 'category',
            boundaryGap: false,
            data: date
          },
          yAxis: {
            boundaryGap: [0, '50%'],
            type: 'value'
          },
          series: [
            {
              name: '成交',
              type: 'line',
              smooth: true,
              symbol: 'none',
              stack: 'a',
              areaStyle: {
                normal: {}
              },
              data: data
            }
          ]
        };

        setInterval(function () {
          addData(true);
          myChart.setOption(option);
        }, 1000);

        window.addEventListener('resize', () => myChart.resize());
      }
    },
    mounted() {
      this.bindEg1();
      this.bindEg2();
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
