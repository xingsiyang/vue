<template>
  <el-row :gutter="20">
    <el-col :span="5">
      <el-container id="leftcontainer">
        <el-header>
          Global Cases<br>9999
        </el-header>
        <el-main style="max-height: 500px">
          <el-table :data="tableData" style="width:auto">
            <el-table-column
              prop="date"
              label="Cases by Province/State/Dependency"
              width="180">
            </el-table-column>
        </el-table>
        </el-main>
        <el-footer>
          12/26/2020 4:21 下午
        </el-footer>
      </el-container>
    </el-col>
    <el-col :span="11">
      <el-container id="midcontainer">
        <el-main id="midmain">
          <Mymap></Mymap>
        </el-main>
        <el-footer height=50px id="midfooter">
          <p>hahahahahhahaha</p>
        </el-footer>
      </el-container>
    </el-col>
    <el-col :span="8">
      <el-container id="rightcontainer">
        <el-main style="max-height: 500px">
          <el-row gutter="10">
            <el-col :span=12>
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
        <el-footer>
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
      tableData: [{
            date: '2016-05-02',
          }, {
            date: '2016-05-03',
          }]
    }
  },
  methods: {
    drawLine: function () {
      let myChart = echarts.init(document.getElementById('lines'));
 
      // 指定图表的配置项和数据
      let option = {
        // tooltip: {},
        xAxis: {
          data: ["衬衫","羊毛衫","雪纺衫","裤子","高跟鞋","袜子"]
        },
        yAxis: {},
        series: [{
          name: '销量',
          type: 'line',
          data: [5, 20, 36, 10, 10, 20]
        }]
      };

      // 使用刚指定的配置项和数据显示图表。
      myChart.setOption(option);
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
  height: 101%;
} 

#leftcontainer {
  background-color: #e4f5ef;
  /* border: 1px solid black; */
  border-radius: 10px
}

#midmain {
  background-color: #e4f5ef;
  /* border: 1px solid black; */
  border-radius: 10px;
  text-align: center;
  padding: 0%;
}

#midfooter{
  margin-top: 10px;
  background-color: #e4f5ef;
  /* border: 1px solid black; */
  border-radius: 10px;
  text-align: center;
}

#rightcontainer {
  background-color: #e4f5ef;
  /* border: 1px solid black; */
  border-radius: 10px
}
</style>
