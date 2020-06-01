<template>
    <div class="home-container">
        <div class="home-content">
            <div class="home-content-left">
              <!-- <p class="home-top-bar">全国就业人口数</p> -->
            <!-- <div class="echarts"> -->
              <div :style="{height:'400px',width:'60%',display:'inline-block'}" ref="myEchart"></div>
            <!-- </div> -->
            <!-- <div class="echarts-bar"> -->
                  <div id="myChartBar" :style="{width: '39%', height: '400px',verticalAlign:'top',display:'inline-block'}"></div>
            <!-- </div> -->
                 
            
           </div>
            <div class="home-content-right">
              <div class="home-left">
                <div id="myChart" :style="{width: '48%', height: '400px',display:'inline-block'}"></div>
            <div id="myChartxz" :style="{width: '50%', height: '400px',display:'inline-block'}"></div>
            </div>
            <div class="home-left">
                <div id="myChartcp" :style="{width: '48%', height: '400px',display:'inline-block'}"></div>
            <div id="myChartxz2" :style="{width: '50%', height: '420px',display:'inline-block'}"></div>
            </div>
                <wordcloud
      :data="defaultWords"
      nameKey="name"
      valueKey="value"
      :color="myColors"
      :showTooltip="true"
      :wordClick="wordClickHandler">
      </wordcloud>
            </div>
            
        </div>
    </div>
</template>

<script>
import wordcloud from "vue-wordcloud";
import echarts from "echarts";
import "../../node_modules/echarts/map/js/china.js"; // 引入中国地图数据
export default {
  name: "home",
  props: ["userJson"],
  data() {
    return {
      myColors: ["#fb9f9c", "#fabd94", "#6b9956", "#c9e0ef", "#d0a7c9"],
      defaultWords: [
        {
          name: "数据分析师",
          value: 26
        },
        {
          name: "数据分析师",
          value: 19
        },
        {
          name: "数据分析师",
          value: 18
        },
        {
          name: "数据分析师",
          value: 16
        },
        {
          name: "数据分析师",
          value: 15
        },
        {
          name: "数据分析师",
          value: 9
        },
        {
          name: "数据分析师",
          value: 9
        },
        {
          name: "good",
          value: 9
        },
        {
          name: "play",
          value: 6
        },
        {
          name: "good",
          value: 19
        },
        {
          name: "play",
          value: 18
        },
        {
          name: "数据分析师",
          value: 16
        },
        {
          name: "数据分析师",
          value: 15
        },
        {
          name: "数据分析师",
          value: 9
        },
        {
          name: "数据分析师",
          value: 9
        },
        {
          name: "good",
          value: 9
        },
        {
          name: "play",
          value: 6
        }
      ],
      dataList: [
        { name: "南海诸岛", value: 80 },
        { name: "北京", value: 100 },
        { name: "天津", value: 990 },
        { name: "上海", value: 100 },
        { name: "重庆", value: 780 },
        { name: "河北", value: 100 },
        { name: "河南", value: 100 },
        { name: "云南", value: 540 },
        { name: "辽宁", value: 100 },
        { name: "黑龙江", value: 100 },
        { name: "湖南", value: 100 },
        { name: "安徽", value: 100 },
        { name: "山东", value: 980 },
        { name: "新疆", value: 120 },
        { name: "江苏", value: 100 },
        { name: "浙江", value: 230 },
        { name: "江西", value: 350 },
        { name: "湖北", value: 100 },
        { name: "广西", value: 90 },
        { name: "甘肃", value: 100 },
        { name: "山西", value: 100 },
        { name: "内蒙古", value: 100 },
        { name: "陕西", value: 60 },
        { name: "吉林", value: 50 },
        { name: "福建", value: 1000 },
        { name: "贵州", value: 100 },
        { name: "广东", value: 100 },
        { name: "青海", value: 100 },
        { name: "西藏", value: 100 },
        { name: "四川", value: 10 },
        { name: "宁夏", value: 500 },
        { name: "海南", value: 100 },
        { name: "台湾", value: 400 },
        { name: "香港", value: 100 },
        { name: "澳门", value: 100 }
      ],
      chinaNameList:["北京","上海","广州","深圳","杭州"
     ],
      chinaValueList:[
        420,330,280,360,160
      ]
    };
  },
  components: {
    wordcloud
  },
  beforeDestroy() {
    if (!this.chart) {
      return;
    }
    this.chart.dispose();
    this.chart = null;
  },
  methods: {
    chinaConfigure() {
      console.log(this.userJson);
      let myChart = echarts.init(this.$refs.myEchart); //这里是为了获得容器所在位置
      window.onresize = myChart.resize;
      myChart.setOption({
        // 进行相关配置
        tooltip: {
          formatter: function(params, ticket, callback) {
            return (
              params.seriesName + "<br />" + params.name + "：" + params.value
            );
          } //数据格式化
        },
        visualMap: {
          min: 0,
          max: 1500,
          left: "left",
          top: "bottom",
          text: ["高", "低"], //取值范围的文字
          inRange: {
            color: [
              "#5475f5",
              "#9feaa5",
              "#85daef",
              "#74e2ca",
              "#e6ac53",
              "#9fb5ea"
            ] //取值范围的颜色
          },
          textStyle: {
            color: "#fff"
          },
          show: true //图注
        },
        geo: {
          map: "china",
          roam: false, //不开启缩放和平移
          zoom: 1.23, //视角缩放比例
          label: {
            normal: {
              show: true,
              fontSize: "10",
              color: "#fff"
            }
          },
          itemStyle: {
            normal: {
              borderColor: "rgba(0, 0, 0, 0.2)"
            },
            emphasis: {
              areaColor: "#1e3d5d", //鼠标选择区域颜色
              shadowOffsetX: 0,
              shadowOffsetY: 0,
              shadowBlur: 20,
              borderWidth: 0,
              shadowColor: "rgba(0, 0, 0, 0.5)"
            }
          }
        },
        series: [
          {
            name: "信息量",
            type: "map",
            geoIndex: 0,
            data: this.dataList
          }
        ]

        // backgroundColor: "#02AFDB",
        // tooltip: {}, // 鼠标移到图里面的浮动提示框
        // dataRange: {
        //   show: false,
        //   min: 0,
        //   max: 1000,
        //   text: ['High', 'Low'],
        //   realtime: true,
        //   calculable: true,
        //   color: ['orangered', 'yellow', 'lightskyblue']
        // },
        // geo: { // 这个是重点配置区
        //   map: 'china', // 表示中国地图
        //   roam: true,
        //   label: {
        //     normal: {
        //       show: true, // 是否显示对应地名
        //       textStyle: {
        //         color: 'rgba(0,0,0,0.4)'
        //       }
        //     }
        //   },
        //   itemStyle: {
        //     normal: {
        //       borderColor: 'rgba(0, 0, 0, 0.2)'
        //     },
        //     emphasis: {
        //       areaColor: null,
        //       shadowOffsetX: 0,
        //       shadowOffsetY: 0,
        //       shadowBlur: 20,
        //       borderWidth: 0,
        //       shadowColor: 'rgba(0, 0, 0, 0.5)'
        //     }
        //   }
        // },
        // series: [{
        //     type: 'scatter',
        //     coordinateSystem: 'geo' // 对应上方配置
        //   },
        //   {
        //     name: '启动次数', // 浮动框的标题
        //     type: 'map',
        //     geoIndex: 0,
        //     data: [{
        //       "name": "北京",
        //       "value": 599
        //     }, {
        //       "name": "上海",
        //       "value": 142
        //     }, {
        //       "name": "黑龙江",
        //       "value": 44
        //     }, {
        //       "name": "深圳",
        //       "value": 92
        //     }, {
        //       "name": "湖北",
        //       "value": 810
        //     }, {
        //       "name": "四川",
        //       "value": 453
        //     }]
        //   }
        // ]
      });
    },
  //china 分布图
  chinaBar() {
      // 基于准备好的dom，初始化echarts实例
      let myChartBar = echarts.init(document.getElementById("myChartBar"));
      // 绘制图表
      myChartBar.setOption({
        title: {
          text: "区域薪资分布图",
          subtext: "",
          textStyle:{
            color:'#fff',
            fontWeight:'normal'
          }
        },
        tooltip: {
          trigger: "axis"
        },
        legend: {
           orient: 'vertical',
          // data: ["博士", "硕士", "本科", "大专", "高中"]
        },
        // toolbox: {
        //   show: true,
        //   feature: {
        //     magicType: { show: true, type: ["line", "bar", "pie"] }
        //   }
        // },
        calculable: true,
        xAxis: [
          {
            type: "value",
            data: this.chinaValueList,
             axisLine:{
			        lineStyle:{
			            color:'#fff',
			            width:1
			        }
          },
          splitLine:{
            show:false
          }
          }
        ],
        yAxis: [
          {
            type: "category",
            // name:'万',
            data:this.chinaNameList,
            axisLabel:{
              interval:0
            },
            axisLine:{
			        lineStyle:{
			            color:'#fff',
			            width:1
			        }
          },
          splitLine:{
            show:false
          }
          }
        ],
        series: [
          {
            // name: "薪资",
            type: "bar",
            data: this.chinaValueList,
            // markPoint: {
            //   data: [
            //     { type: "max", name: "最大值" },
            //     { type: "min", name: "最小值" }
            //   ]
            // },
            // markLine: {
            //   data: [{ type: "average", name: "平均值" }]
            // },
            itemStyle:{
              normal:{
                // label:{
                //   show:true,
                //   position:top,
                // },
                //   textStyle:{
                   
                //   }
                // }
                color:"#235a92",
                label:{
                   
                   show:true,
                   position:'right',
                   textStyle:{
                     color:"#fff",
                     fontSize:16
                   }
                }
              }
            }
          }
        ]
      });
    },
    wordClickHandler(name, value, vm) {
      console.log("wordClickHandler", name, value, vm);
    },
    drawLine() {
      // 基于准备好的dom，初始化echarts实例
      let myChart = echarts.init(document.getElementById("myChart"));
      // 绘制图表
      
      myChart.setOption({
        title: {
          text: "就业人口学历图",
          subtext: "",
          left: "center",
          textStyle:{
            color:'#fff',
            fontWeight:'normal'
          }
        },
        tooltip: {
          trigger: "item",
          formatter: "{a} <br/>{b} : {c} ({d}%)"
        },
        // legend: {
        //   left: "center",
        //   top: "bottom",
        //   data: ["大专", "本科", "硕士", "博士"]
        // },
        toolbox: {
          show: true,
          feature: {
            mark: { show: true }
          }
        },
        series: [
          {
            name: "学历",
            type: "pie",
            radius: [30, 70],
            center: ["45%", "50%"],
            roseType: "area",
            data: [
              { value: 10, name: "大专" },
              { value: 5, name: "本科" },
              { value: 15, name: "硕士" },
              { value: 25, name: "博士" }
            ],
            itemStyle:{
              normal:{
                color:function(params){
                  var colorList = ["#32b5cb","#0cb49b","#fb5051","#b1f33f"];
                  console.log(colorList[params.dataIndex],'color')
                  return colorList[params.dataIndex]
                }
              }
            }
          }
        ]
      });
    },
    // 学历薪资图
    drawxz() {
      // 基于准备好的dom，初始化echarts实例
      let myChartxz = echarts.init(document.getElementById("myChartxz"));
      // 绘制图表
      myChartxz.setOption({
        title: {
          text: "学历与薪资分布图",
          subtext: "",
          textStyle:{
            color:'#fff',
            fontWeight:'normal'
          }
        },
        tooltip: {
          trigger: "axis"
        },
        legend: {
          data: ["博士", "硕士", "本科", "大专", "高中"]
        },
        toolbox: {
          show: true,
          feature: {
            magicType: { show: true, type: ["line", "bar", "pie"] }
          }
        },
        calculable: true,
        xAxis: [
          {
            type: "category",
            data: ["博士", "硕士", "本科", "大专", "高中"],
             axisLine:{
			        lineStyle:{
			            color:'#fff',
			            width:2
			        }
			    },
          }
        ],
        yAxis: [
          {
            type: "value",
            name:'万',
            // axisLabel:{
            //   formatter:"{value}(万)"
            // },
            axisLine:{
			        lineStyle:{
			            color:'#fff',
			            width:2
			        }
			    },
          }
        ],
        series: [
          {
            name: "薪资",
            type: "bar",
            data: [0.4, 5, 8, 10, 13],
            markPoint: {
              data: [
                { type: "max", name: "最大值" },
                { type: "min", name: "最小值" }
              ]
            },
            markLine: {
              data: [{ type: "average", name: "平均值" }]
            },
            itemStyle:{
              normal:{
                color:"#235a92"
              }
            }
          }
        ]
      });
    },
    // 公司类型对应岗位数
    drawcp() {
      // 基于准备好的dom，初始化echarts实例
      let myChartcp = echarts.init(document.getElementById("myChartcp"));
      // 绘制图表
      myChartcp.setOption({
        title: {
          text: "公司类型对应岗位数",
          subtext: "",
          left: "center",
           textStyle:{
            color:'#fff',
            fontWeight:'normal'
          }
        },
        tooltip: {
          trigger: "item",
          formatter: "{a} <br/>{b} : {c} ({d}%)"
        },
        // legend: {
        //   orient: "vertical",
        //   left: "left",
        //   data: [
        //     "民营",
        //     "上市",
        //     "合资",
        //     "国企",
        //     "外资",
        //     "创业",
        //     "事业",
        //     "非盈利",
        //     "外企",
        //     "政府"
        //   ]
        // },
        series: [
          {
            name: "公司类型",
            type: "pie",
            radius: "55%",
            center: ["50%", "60%"],
            data: [
              { value: 335, name: "民营" },
              { value: 310, name: "上市" },
              { value: 234, name: "合资" },
              { value: 135, name: "国企" },
              { value: 1548, name: "外资" },
              { value: 1548, name: "创业" },
              { value: 1548, name: "事业" },
              { value: 1548, name: "非盈利" },
              { value: 1548, name: "外企" },
              { value: 1548, name: "政府" }
            ],
            emphasis: {
              itemStyle: {
                shadowBlur: 10,
                shadowOffsetX: 0,
                shadowColor: "rgba(0, 0, 0, 0.5)"
              }
            }
          }
        ]
      });
    },
    // 公司对应薪资
    drawxz2() {
      // 基于准备好的dom，初始化echarts实例
      let myChartxz2 = echarts.init(
        document.getElementById("myChartxz2")
      );
      // 绘制图表
      myChartxz2.setOption({
        title: {
          text: "公司类型对应薪资",
          subtext: "",
          left: "center",
           textStyle:{
            color:'#fff',
            fontWeight:'normal'
          }
        },
        xAxis: {
          type: "category",
          data: [
            "民营",
            "上市",
            "合资",
            "国企",
            "外资",
            "创业",
            "事业",
            "非盈利",
            "外企",
            "政府"
          ],
          axisLine:{
			        lineStyle:{
			            color:'#fff',
			           
			        }
          },
        },
        yAxis: {
          type: "value",
          name:'万',
          axisLine:{
			        lineStyle:{
			            color:'#fff',
			            
			        }
          },
          
        },
        series: [
          {
            data: [8, 13, 1, 4, 9, 10, 1.3, 8, 10, 13],
            type: "line",
            itemStyle:{
              normal:{
                color:'#61a0a8'
              }
            }
            
          }
        ]
      });
    }
  },
  mounted() {
    this.chinaConfigure();
    this.chinaBar();
    this.drawLine();
    this.drawxz();
    this.drawcp();
    this.drawxz2();
  }
};
</script>

<style scoped>
.home-container {
  padding: 10px;
  padding-top: 5px;
}
.home-content {
  padding: 10px;
  border-radius: 5px;
  /* background: #fff; */
}
.home-left {
  width: 50%;
  /* border: 1px solid #afa; */
  display:inline-block;
  float:left
}
.home-content-left {
  width: 100%;
  height:50%;
  display: inline-block;
}
/* .echarts{
  width:60%;
  display:inline-block;
}
.echarts-bar{
  width:40%;
  display:inline-block;
} */
.home-top-bar{
  width:300px;
  height:40px;
  background:rgba(41,119,199,0.5);
  color:#fff;
}
.home-content-right {
  width: 100%;
  height:50%;
  float: right;
  display: inline-block;
}
.amap-wrapper {
  width: 500px;
  height: 500px;
}
</style>