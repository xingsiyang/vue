<template>
  <el-row :gutter="15">
    <el-col :span="5">
      <el-container id="leftcontainer">
        <el-header id="leftheader">
          Global Cases<br>9999
        </el-header>
        <el-main id="leftmain">
          <el-form>
            <el-form-item v-for="site in tableData">{{ site.date }}</el-form-item>
          </el-form>
        </el-main>
        <el-footer id="leftfooter">
          上次刷新时间
          <br>
          {{ new Date().toLocaleString( ) }}
        </el-footer>
      </el-container>
    </el-col>
    <el-col :span="11">
      <el-container id="midcontainer">
        <el-main id="midmain">
          <Mymap @child='update'></Mymap>
        </el-main>
        <el-footer height=10% id="midfooter">
          <p>hahahahahhahaha</p>
        </el-footer>
      </el-container>
    </el-col>
    <el-col :span="8">
      <el-container id="rightcontainer">
        <el-container id="righttop">
          <el-aside id="rightaside" width="47%">
            <el-form>
              <el-form-item v-for="site in tableData">{{ site.date }}</el-form-item>
            </el-form>
          </el-aside>
          <el-main id="rightmain">
            <el-form>
              <el-form-item v-for="site in tableData">{{ site.date }}</el-form-item>
            </el-form>
          </el-main>
        </el-container>
        <el-footer id="rightfooter" height=30%>
          <div id="lines" style="width: 100%; height: 100%;"></div>
        </el-footer>
      </el-container>
    </el-col>
  </el-row>
</template>

<script>
import Mymap from './Map'

function getdata(context,url)
{
  var xmlhttp;
  if (window.XMLHttpRequest)
  {// code for IE7+, Firefox, Chrome, Opera, Safari
    xmlhttp=new XMLHttpRequest();
  }
  else
  {// code for IE6, IE5
    xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
  }
  xmlhttp.onreadystatechange=function()
  {
    if (xmlhttp.readyState==4 && xmlhttp.status==200)
    {
      if (url == "api/all")
      {
        context.init(JSON.parse(xmlhttp.responseText));
      }
      // return xmlhttp.responseText;
      // alert(xmlhttp.responseText)
      // update(JSON.parse(xmlhttp.responseText));
    }
  }
  xmlhttp.open("GET","http://47.95.198.55:3001/" + url,true);
  xmlhttp.send();
}

export default {
  name: 'Home',
  data() {
    return{
      tableData: [],
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
    init: function (data) {
      let newTable = [];
      for (let i = 0; i < data.length; i++)
      {
        newTable.push({'date': data[i].name})
      }
      for (let i = 0; i < data.length; i++)
      {
        newTable.push({'date': data[i].name})
      }
      this.tableData = newTable;
    },
    drawLine: function (option) {
      let myChart = echarts.init(document.getElementById('lines'));
      // 使用指定的配置项和数据显示图表。
      myChart.setOption(option);
    },
    update: function (data) {
      alert(data)
    }
  },
  mounted(){
    this.drawLine(this.option);
    getdata(this,'api/all');
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
  margin-top: 3%;
}

#leftfooter {
  background-color: #e4f5ef;
  border-radius: 10px;
  height: 10%!important;
  margin-top: 3%;
  text-align: center;
  padding: 3%;
}

#midmain {
  background-color: #e4f5ef;
  border-radius: 10px;
  text-align: center;
  padding: 0%;
}

#midfooter{
  margin-top: 1.2%;
  background-color: #e4f5ef;
  border-radius: 10px;
  text-align: center;
}

#righttop {
  height: 70%;
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
  margin-top: 2%;
  padding-top: 5%;
  text-align: center;
}
</style>