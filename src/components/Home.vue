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
    <el-col :span="14">
      <el-container id="midcontainer">
        <el-main>
          <Mymap></Mymap>
        </el-main>
        <el-footer height=50px>
          <p>hahahahahhahaha</p>
        </el-footer>
      </el-container>
    </el-col>
    <el-col :span="5">
      <el-container id="rightcontainer">
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
          这是一个图
        </el-footer>
      </el-container>
    </el-col>
  </el-row>
</template>

<script>
import Mymap from './Map'

export default {
  name: 'Home',
  data() {
    return{
      tableData: [{
            date: '2016-05-02',
          }, {
            date: '2016-05-04',
          }, {
            date: '2016-05-04',
          }, {
            date: '2016-05-04',
          }, {
            date: '2016-05-04',
          }, {
            date: '2016-05-04',
          }, {
            date: '2016-05-04',
          }, {
            date: '2016-05-04',
          }, {
            date: '2016-05-04',
          }, {
            date: '2016-05-04',
          }, {
            date: '2016-05-01',
          }, {
            date: '2016-05-03',
          }]
    }
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

#leftcontainer {
  background-color: white;
}

#midcontainer {
  background-color: white;
  text-align: center;
}

#rightcontainer {
  background-color: white;
}
</style>