<template>
  <el-row :gutter="15">
    <el-col :span="5">
      <el-container id="leftcontainer">
        <el-header id="leftheader">
          Global Cases<br>9999
        </el-header>
        <el-main id="leftmain">
          <el-table :data="tableData" style="width:auto">
            <el-table-column
              prop="date"
              label="Cases by Province/State/Dependency"
              width="180">
            </el-table-column>
        </el-table>
        </el-main>
        <el-footer id="leftfooter">
          12/26/2020 4:21 下午
        </el-footer>
      </el-container>
    </el-col>
    <el-col :span="11">
      <el-container id="midcontainer">
        <el-main id="midmain">
          <Mymap></Mymap>
        </el-main>
        <el-footer height=10% id="midfooter">
          <p>hahahahahhahaha</p>
        </el-footer>
      </el-container>
    </el-col>
    <el-col :span="8">
      <el-container id="rightcontainer">
        <el-main id="rightmain">
          <el-row :gutter="10">
            <el-col :span="12">
              <el-table :data="tableData" style="width: 100%">
                <el-table-column
                  prop="date"
                  label="Cases by Province/State/Dependency"
                  width="180">
                </el-table-column>
              </el-table>
            </el-col>
            <el-col :span="12">
              <el-table :data="tableData" style="width: 100%">
                <el-table-column
                  prop="date"
                  label="Cases by Province/State/Dependency"
                  width="180">
                </el-table-column>
              </el-table>
            </el-col>
          </el-row>
        </el-main>
        <el-footer id="rightfooter">
          <div id="lines" style="width: 100%; height: 100%;"></div>
        </el-footer>
      </el-container>
    </el-col>
  </el-row>
</template>

<script>
import Mymap from './Map'
let echarts = require('echarts');

export default {
  name: 'Home',
  data() {
    return{
      tableData: [
        {
          date: '2016-05-02',
        }, {
          date: '2016-05-03',
        }
      ],
      option: {
        title: {
          text: 'ECharts 入门示例'
        },
        tooltip: {},
        legend:{
            data:['销量','aa']
        },
        xAxis: {
          data: ["衬衫","羊毛衫","雪纺衫","裤子","高跟鞋","袜子"]
        },
        yAxis: {},
        series: [
          {
            name: '销量',
            type: 'line',
            data: [5, 20, 36, 10, 10, 20]
          },
          {
            name: 'aa',
            type: 'line',
            data: [5, 20, 36, 10, 15, 20]
          }
      ]
      }
    }
  },
  methods: {
    drawLine: function () {
      let myChart = echarts.init(document.getElementById('lines'));
      // 使用指定的配置项和数据显示图表。
      myChart.setOption(this.option);
    }
  },
  mounted(){
    this.drawLine();
  },
  components: {
    Mymap
  }
}
</script>

<style>
.el-row {
  height: 100%;
}

.el-col {
  height: 100%;
}

.el-container {
  height: 100%;
} 

#leftheader {
  background-color: #e4f5ef;
  height: 15%!important;
  border-radius: 10px
}

#leftmain {
  background-color: #e4f5ef;
  border-radius: 10px;
  height: 75%!important;
  margin-top: 10px;
}

#leftfooter {
  background-color: #e4f5ef;
  border-radius: 10px;
  height: 10%!important;
  margin-top: 10px;
}

#midmain {
  background-color: #e4f5ef;
  border-radius: 10px;
  text-align: center;
  padding: 0%;
}

#midfooter{
  margin-top: 10px;
  background-color: #e4f5ef;
  border-radius: 10px;
  text-align: center;
}

#rightmain{
  background-color: #e4f5ef;
  border-radius: 10px
}

#rightfooter {
  background-color: #e4f5ef;
  border-radius: 10px;
  margin-top: 10px;
  height: 30%!important;
  padding-top: 5%;
}
</style>