<template>
  <el-row :gutter="15">
    <el-col :span="5">
      <el-container id="leftcontainer">
        <el-header id="leftheader" style="text-align: center; padding-top: 5%;">
          全美总感染人数<br><br>{{ totalconfirmed }}
        </el-header>
        <el-main id="leftmain">
          <el-container>
            <el-header height="10%" style="text-align: center;">
              <div style="text-align: center; height: 100%; padding:5% 0px;">各州感染数</div>
            </el-header>
            <el-main style="padding-top: 0px;">
              <el-form>
                <el-form-item v-for="site in leftmid">{{ site.province }} : {{ site.case }} Cases</el-form-item>
              </el-form>
            </el-main>
          </el-container>
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
          <Mymap @child='select'></Mymap>
        </el-main>
        <el-footer height=10% id="midfooter">
          <p v-if="currentcity==''">请从地图上选择一个美国城市</p>
          <p v-else-if="startday==''">暂时只支持美国的城市</p>
        </el-footer>
      </el-container>
    </el-col>
    <el-col :span="8">
      <el-container id="rightcontainer">
        <el-container id="righttop">
          <el-aside id="rightaside" width="47%">
            <el-container>
              <el-header height="25%" style="text-align: center;">
                <div style="text-align: center; height: 100%; padding:5% 0px;">{{ currentcity }} {{ currentprovince }} <br><br> 对十天内确诊人数的预测：</div>
              </el-header>
              <el-main style="padding-top: 0px;" v-if="endday!=''">
                <el-form>
                  <el-form-item v-for="site in rightl">{{ site.date }} - {{ site.case }}</el-form-item>
                </el-form>
              </el-main>
            </el-container>
          </el-aside>
          <el-main id="rightmain">
            <el-container>
              <el-header height="10%" style="text-align: center;">
                <div style="text-align: center; height: 100%; padding:5% 0px;">{{ currentprovince }}</div>
              </el-header>
              <el-main style="padding-top: 0px;">
                <el-form>
                  <el-form-item v-for="site in rightr" style="margin-bottom: 5%;">{{ site.city }} : {{ site.case }}</el-form-item>
                </el-form>
              </el-main>
              <el-footer height="5%" style="margin-top:3%;">
                <el-radio-group v-model="radio" @change="changestate">
                  <el-radio :label="'confirmed'">确诊数</el-radio>
                  <el-radio :label="'death'">死亡数</el-radio>
                </el-radio-group>
              </el-footer>
            </el-container>
          </el-main>
        </el-container>
        <el-footer id="rightfooter" height=28%>
          <div id="lines" style="width: 100%; height: 100%;"></div>
        </el-footer>
      </el-container>
    </el-col>
  </el-row>
</template>

<script>
import Mymap from './Map'

function getdata(context,url,state)
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
      if (state == 0)
      {
        context.updateleft(JSON.parse(xmlhttp.responseText));
      }
      else if (state == 1)
      {
        context.updaterightr(JSON.parse(xmlhttp.responseText));
      }
      else if (state == 2)
      {
        context.updaterightbottom(JSON.parse(xmlhttp.responseText)); 
      }
      else if (state == 3)
      {
        context.updaterightl(JSON.parse(xmlhttp.responseText)); 
      }
    }
  }
  xmlhttp.open("GET","http://47.95.198.55:8000/" + url,true);
  xmlhttp.send();
}

function addDate (startday, length)
{
  let dateList = [];
  let date = new Date(startday);
  for (let i = 0; i < length; i++)
  {
    dateList.push(date.toLocaleDateString())
    date = date.setDate(date.getDate()+1);
    date=new Date(date);
  }
  return dateList;
}

function setFormatDate (day)
{
  let str = day.split("/")
  if (str[0].length == 1)
  {
    str[0] = '0' + str[0]
  }
  if (str[1].length == 1)
  {
    str[1] = '0' + str[0]
  }
  str[2] = '20' + str[2]
  return str[2] + '-' + str[0] + '-' + str[1]
}

export default {
  name: 'Home',
  data() {
    return{
      radio: "confirmed",
      totalconfirmed: 0,
      currentprovince: '',
      currentcity: '',
      prodictday: [],
      startday: ' ',
      endday: '',
      leftmid: [],
      rightr: [],
      rightl: [],
      option: {
        title: {
          text: ''
        },
        tooltip: {},
        legend:{
            data:['死亡数','确诊数']
        },
        xAxis: {
          data: []
        },
        yAxis: {},
        series: [
          {
            name: '死亡数',
            type: 'bar',
            data: []
          },
          {
            name: '确诊数',
            type: 'bar',
            data: []
          }
      ]
      }
    }
  },
  methods: {
    updateleft: function (res) {
      let newleftmid = [];
      let count = 0;
      for (let i = 0; i < res.data.length; i++)
      {
        let item = [];
        item['province'] = res.data[i].province;
        item['case'] = res.data[i].confirmed;
        count += res.data[i].confirmed;
        newleftmid.push(item)
      }
      this.leftmid = newleftmid;
      this.totalconfirmed = count
    },
    updaterightr: function (res) {
      let newrightr = [];
      for (let i = 0; i < res.data.length; i++)
      {
        let item = [];
        item['city'] = res.data[i].city;
        if (this.radio == 'confirmed')
        {
          item['case'] = res.data[i].confirmed;
        }
        else if (this.radio == 'death')
        {
          item['case'] =parseInt(res.data[i].death * 0.4);
        }
        newrightr.push(item)
      }
      this.rightr = newrightr;
    },
    updaterightl:function (res) {
      let newrightl = [];
      let dates = addDate(this.endday, 11);
      for (let i = 0; i < res.predicted_value.length; i++)
      {
        let item = [];
        item['case'] = parseInt(res.predicted_value[i]);
        item['date'] = dates[i + 1]
        newrightl.push(item)
      }
      this.rightl= newrightl;
    },
    updaterightbottom: function (res) {
      this.option.title.text = this.currentcity;
      let x = [];
      let dy = [];
      let cy = [];
      this.startday = '';
      this.endday = '';
      if (res.result.length > 0)
      {
        this.startday = setFormatDate(res.result[0].X)
        x = addDate(this.startday, res.result[0].Y.length);
        for (let i = 0; i < res.result[0].Y.length; i++)
        {
          dy.push(parseInt(res.result[0].Y[i] * 0.4))
          cy.push(res.result[1].Y[i + 1])
        }
        this.endday = x[x.length - 1]
      }
      this.option.xAxis.data = x;
      this.option.series[0].data = dy;
      this.option.series[1].data = cy;
      this.drawLine(this.option);
    },
    drawLine: function (option) {
      let myChart = echarts.init(document.getElementById('lines'));
      // 使用指定的配置项和数据显示图表。
      myChart.setOption(option);
    },
    changestate: function (res) {
      if (this.currentprovince != '')
      {
        getdata(this,'listcity?type=' + this.radio + '&state=' + this.currentprovince,1);
      }
    },
    select: function (data) {
      this.currentprovince = data.province;
      this.currentcity = data.city;
      getdata(this,'listcity?type=' + this.radio + '&state=' + this.currentprovince,1);
      getdata(this,'quary?&c=' + this.currentcity + '&p=' + this.currentprovince,2); 
      getdata(this,'prodict?&p=' + this.currentprovince + '&c=' + this.currentcity + '&type=confirmed&len=10',3);   
    }
  },
  mounted(){
    getdata(this,'state',0);
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
  padding: 0px;
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