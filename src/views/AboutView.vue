<template>
  <div class="aaa">
    <div style="display:flex;justify-content: space-around;margin:100px 0px 0px 0px;position: absolute;width: 100%;">
      <div @click="one()"
        class="view">
        <p>one {{pv}}</p>
        <div id="chart_example">
                  
        </div>
      </div>
      <div @click="tow()"
        class="view">

        <p>tow {{pv}}</p>
      </div>
    </div>
    <span class="span"></span>
    <div>
      <div class="view" style="width:98.8%;position: absolute;">

      </div>
    </div>
</div>
</template>

<script>
//echarts 5的版本引入方式
import * as echarts from 'echarts';
export default {

  data(){
    return{
      pv:"访问量"
    }
  },
  mounted() {
    let this_ = this;
    let myChart = echarts.init(document.getElementById('chart_example'));
    let option = {
            color: ['#c7e0f4'],
            tooltip : {
              trigger: 'axis',
              axisPointer : {
                type : 'shadow'
              }
            },
            xAxis : [
              {
                type : 'category',
                data : ['1月','2月','3月','4月','5月','6月','7月','8月','9月','10月','11月','12月',],
                axisTick: {
                  alignWithLabel: true
                }
              }
            ],
            yAxis : [
              {
                type : 'value'
              }
            ],
            series : [
              {
                name:'每月花费',
                type:'bar',
                barWidth: '60%',
                data:[995,666,444,858,654,236,645,546,846,225,547,356]
              }
            ]
      };
      myChart.setOption(option);
 
      //建议加上以下这一行代码，不加的效果图如下（当浏览器窗口缩小的时候）。超过了div的界限（红色边框）
      window.addEventListener('resize',function() {myChart.resize()});
    },
  methods:{
    one(){
      this.$router.push({path:"/home/HomeView/one"})
    },
    tow(){
       this.$router.push({path:"/home/HomeView/tow"})
    },
    drawLine(){
        // 基于准备好的dom，初始化echarts实例
        let myChart = echarts.init(document.getElementById('myChart'))
        // 绘制图表
        myChart.setOption({
            title: { text: '在Vue中使用echarts' },
            tooltip: {},
            xAxis: {
                data: ["衬衫","羊毛衫","雪纺衫","裤子","高跟鞋","袜子"]
            },
            yAxis: {},
            series: [{
                name: '销量',
                type: 'bar',
                data: [5, 20, 36, 10, 10, 20]
            }]
        });
    }
  },
   watch: {},
    created() {
 
    }
}
</script>

<style>
#chart_example{
    width: 80%;
    height: 80%;
    margin: 0 auto;
  }
*::-webkit-scrollbar {
				display: none;
	}
.span{
  width: 100%;
  height: calc(50vh + 100px);
  display: block;
}
.aaa{
  overflow: auto;
  position: relative;
  width: 100%;
  height: calc(100vh - 100px);
  background: url('../assets/wallhaven-gjmyl7.jpg') no-repeat;
  background-position: center 0;
  background-size: cover;
}
.mbx{
  font-size: 16px;
  padding: 17px;
  text-align: center;
  height: 18px;
  width: 100%;
}.view{
  margin:0px 0px 0px 10px;
  text-align: center;
  width: 40%;
  height: 40vh;
  background: rgba( 255, 255, 255, 0.25 );
  box-shadow: 0 8px 32px 0 rgba( 31, 38, 135, 0.37 );
  backdrop-filter: blur( 4px );
  -webkit-backdrop-filter: blur( 4px );
  border-radius: 10px;
  border: 1px solid rgba( 255, 255, 255, 0.18 );
  
}
</style>