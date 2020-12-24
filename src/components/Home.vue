<template> 
	<div id="container"></div> 
</template>

<script> 
export default {
  name: 'Home', 
  methods: { 
    drawMap: function () { 
      // 创建地图实例  =
      var map = new window.BMap.Map("container");
      // 创建点坐标  
      var point = new window.BMap.Point(116.404, 39.915);
      // 初始化地图，设置中心点坐标和地图级别  
      map.centerAndZoom(point, 5);
      // 允许鼠标滚轮缩放
      map.enableScrollWheelZoom(true);

      map.addEventListener('click', function (e) {
        let myGeo = new window.BMap.Geocoder();
        let currentPoint = new window.BMap.Point(e.point.lng, e.point.lat);
        myGeo.getLocation(currentPoint, function(info){
            alert(info.addressComponents.province)
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
#container { 
  height: 99vh;
}   
</style>