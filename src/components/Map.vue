<template>
    <div id="map">这是一个地图</div> 
</template>

<script>
export default {
  name: 'Mymap', 
  methods: {      
    drawMap: function (context) { 
      // 创建地图实例  =
      var map = new window.BMap.Map("map");
      // 创建点坐标  
      var point = new window.BMap.Point(-98.781842,53.441022);
      // 初始化地图，设置中心点坐标和地图级别  
      map.centerAndZoom(point, 5);
      // 允许鼠标滚轮缩放
      map.enableScrollWheelZoom(true);
      map.disableDoubleClickZoom(true)
      map.setMapStyle({     
        styleId: '9ef31e5c6b24670209565799a202515b'
      });

      // 点击事件
      map.addEventListener('click', function (e) {
        let myGeo = new window.BMap.Geocoder();
        let currentPoint = new window.BMap.Point(e.point.lng, e.point.lat);
        myGeo.getLocation(currentPoint, function(info){
          let msg = [];
          msg['city'] = info.addressComponents.city;
          msg['province'] = info.addressComponents.province;
          context.$emit('child',msg)
        })
      });
    } 
  }, 
  mounted(){ 
    //调用上面的函数
    this.drawMap(this) 
  } 
} 
</script>

<style>
#map { 
  height: 100%;
  width: 100%;
}
</style>