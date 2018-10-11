<!DOCTYPE html>
<html lang="zh-cmn-Hans">
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width,initial-scale=1,user-scalable=0">
    <title>导航去</title>
    <script type="text/javascript" src="http://api.map.baidu.com/api?v=2.0&ak=6ZHAx0BAOdsXX7Gp2KkAWkSqw01KmqsP"></script>  
    <script src="http://cdn.bootcss.com/jquery/1.11.1/jquery.min.js"></script><!--调用jQuery-->

  <style type="text/css">
        body, html,#allmap {width: 100%;height: 100%;overflow: hidden;margin:0;font-family:"微软雅黑";}
    </style> 

</head>

<body>  
   <div id="allmap"></div>
</body>  
</html>  
<script type="text/javascript">  

    var map = new BMap.Map("allmap");  
    var point = new BMap.Point(115.7406594221,28.7297295047);
    map.centerAndZoom(point, 16);  
    map.enableScrollWheelZoom(); 

    var myIcon = new BMap.Icon("myicon.png",new BMap.Size(30,30),{
        anchor: new BMap.Size(10,10)    
    });

    var marker=new BMap.Marker(point,{icon: myIcon});  
    map.addOverlay(marker);  

    var geolocation = new BMap.Geolocation();
    geolocation.getCurrentPosition(function(r){
        if(this.getStatus() == BMAP_STATUS_SUCCESS){
            var mk = new BMap.Marker(r.point);
            map.addOverlay(mk);
            //map.panTo(r.point);//地图中心点移到当前位置
            var latCurrent = r.point.lat;
            var lngCurrent = r.point.lng;
            //alert('我的位置：'+ latCurrent + ',' + lngCurrent);

            location.href="http://api.map.baidu.com/direction?origin="+latCurrent+","+lngCurrent+"&destination=28.7297295047,115.7406594221&mode=driving&region=南昌&output=html";

        }
        else {
            alert('failed'+this.getStatus());
        }        
    },{enableHighAccuracy: true})


    map.addOverlay(marker);  
    var licontent="<b>洪福梅岭世纪园</b>"; 
    licontent+="<span><strong>地址：</strong>梅岭</span><br>";
         
    var opts = { 
        width : 200,
        height: 80,
    };         
    var  infoWindow = new BMap.InfoWindow(licontent, opts);  
    marker.openInfoWindow(infoWindow);  
    marker.addEventListener('click',function(){
        marker.openInfoWindow(infoWindow);
    });  

</script>

