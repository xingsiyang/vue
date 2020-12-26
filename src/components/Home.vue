<template>
  <el-row :gutter="15">
    <el-col :span="5">
      <el-container id="leftcontainer">
        <el-header id="leftheader">
          Global Cases<br>9999
        </el-header>
        <el-main id="leftmain">
          <el-table :data="tableData" header-cell-style="background-color: #e4f5ef;" cell-style="background-color: #e4f5ef;">
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
        <el-container>
          <el-aside id="rightaside" width="47%">
            <el-table :data="tableData" header-cell-style="background-color: #e4f5ef;" cell-style="background-color: #e4f5ef;">
              <el-table-column
                prop="date"
                label="Cases by Province/State/Dependency"
                width="180"
                >
              </el-table-column>
            </el-table>
          </el-aside>
          <el-main id="rightmain">
            <el-table :data="tableData" header-cell-style="background-color: #e4f5ef;" cell-style="background-color: #e4f5ef;">
              <el-table-column
                prop="date"
                label="Cases by Province/State/Dependency"
                width="180"
                >
              </el-table-column>
            </el-table>
          </el-main>
        </el-container>
        <el-footer id="rightfooter" height=30%>
          <div id="lines" style="width: 100%; height: 24vh;"></div>
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
        }, {
          date: '2016-05-03',
        }, {
          date: '2016-05-03',
        }, {
          date: '2016-05-03',
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
            data: ['1','2','3','4','5','6']
          },
          {
            name: 'aa',
            type: 'line',
            data: ['1','3','3','5','5','6']
          }
      ]
      }
    }
  },
  methods: {
    drawLine: function (option) {
      let myChart = echarts.init(document.getElementById('lines'));
      // 使用指定的配置项和数据显示图表。
      myChart.setOption(option);
    }
  },
  mounted(){
    this.drawLine(this.option);
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

.el-table {
  background-color: #e4f5ef!important;
  width: 100%!important;
  height: 100%!important;
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
  border-radius: 10px;
  padding: 3%;
}

#rightaside{
  background-color: #e4f5ef;
  border-radius: 10px;
  padding: 3%;
  margin-right: 3%;
}

#rightfooter {
  background-color: #e4f5ef;
  border-radius: 10px;
  margin-top: 10px;
  padding-top: 5%;
  text-align: center;
}
</style>