<template> 
  <div id="container">
    <div id="map"></div> 
  </div>
</template>

<script>

function getdata()
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
      alert(xmlhttp.responseText)
      // update(JSON.parse(xmlhttp.responseText));
    }
  }
  xmlhttp.open("GET","http://49.232.221.85/affair/salary?action=list_salary",true);
  xmlhttp.send();
}

export default {
  name: 'Home', 
  methods: {      
    drawMap: function () { 
      // 创建地图实例  =
      var map = new window.BMap.Map("map");
      // 创建点坐标  
      var point = new window.BMap.Point(116.404, 39.915);
      // 初始化地图，设置中心点坐标和地图级别  
      map.centerAndZoom(point, 5);
      // 允许鼠标滚轮缩放
      map.enableScrollWheelZoom(true);
      // map.setMapStyleV2({     
      //   styleId: '9ef31e5c6b24670209565799a202515b'
      // });

      // 点击事件
      map.addEventListener('click', function (e) {
        let myGeo = new window.BMap.Geocoder();
        let currentPoint = new window.BMap.Point(e.point.lng, e.point.lat);
        myGeo.getLocation(currentPoint, function(info){
            alert(info.addressComponents.province)
            getdata();
        })
      });
    } 
  }, 
  mounted(){ 
    //调用上面的函数
    this.drawMap() 
  } 
} 
</script> 

<style>
#map { 
  height: 80vh;
  width: 40vw;
}   
</style>