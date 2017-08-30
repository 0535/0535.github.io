---
layout: post
title: 一些htm代码
category: 资源
tags: htm
keywords: htm
---

## filedset & legend

```
<!DOCTYPE HTML>
<html>
<body>
  <fieldset>
    <legend>健康信息</legend>
    身高：<input type="text" />
    体重：<input type="text" />
  </fieldset>
  <fieldset style="width:300px;height:150px;border:2px red groove" align=center>
    <legend style="text-align:left;">系统默认</legend>
  </fieldset>
  <fieldset style="width:300px;height:150px;border:1px groove red;Background-color:#ff9966;" align="left" >
    <legend style="width:100px;border:1px dashed #ff9966;background-color:#ff0000;text-align:center;font-family:arial;font-weight:bold;">
      样式4
    </legend> 
   </fieldset> 
</body>
```

演示地址：[W3C](http://www.w3school.com.cn/tiy/t.asp?f=html_fieldset)

## 按钮特效

[Buttons css hover effect](http://pan.baidu.com/s/1hr6pYDY)

![按钮特效](http://pic.yupoo.com/bztd/gVM6Fscw/68029b2b.jpg)

## 时间线

[Vertical timeline](http://pan.baidu.com/s/1dFKP8UP)

![垂直时间线](http://pic.yupoo.com/bztd/gVM6G07T/a8b725a8.jpg)

## 电子地图及Console示例

```
<!doctype html>
<html>
<head>
<meta charset="utf-8">
<title>电子地图及Console示例</title>
<script type="text/javascript" src="http://api.map.baidu.com/api?v=2.0&ak=DDd05fcba9fea5b83bf648515e04fc4c"></script>
<script type="text/javascript" src="http://api.map.baidu.com/library/SearchInfoWindow/1.5/src/SearchInfoWindow_min.js"></script>
<link rel="stylesheet" href="http://api.map.baidu.com/library/SearchInfoWindow/1.5/src/SearchInfoWindow_min.css" />
</head>
<body style="margin:0px; padding:5px; width:100%; height:100%;font-family:"微软雅黑";">
<fieldset style="width:500px">
  <legend>地图标注</legend>
  <div style="width:100%; height:500px; position:relative" id="mapbody"></div>
  <div id="panelWrap">
    <div id="panel"></div>
  </div>
</fieldset>
<hr/>

</body>
</html>
<script type="text/javascript">
//http://developer.baidu.com/map/jsdemo.htm#d0_4 创建信息窗口
var map = new BMap.Map("mapbody");
var point = new BMap.Point(120.431947,37.36884);
var zoom = 18;
map.centerAndZoom(point,zoom);
map.addControl(new BMap.NavigationControl()); 
map.addControl(new BMap.ScaleControl()); 
map.addControl(new BMap.OverviewMapControl());  
map.enableScrollWheelZoom();
map.addControl(new BMap.MapTypeControl());
var content = '<div>地址：你猜猜<br>服务电话：152********</div>';
 
//创建检索信息窗口对象
var searchInfoWindow = null;
searchInfoWindow = new BMapLib.SearchInfoWindow(map, content, {
    title  : "这个是标题框", 
    width  : 150,            
    height : 40,              
    panel  : "panel",         
    enableAutoPan : true,    
    searchTypes   :[
    ]
});

//创建标记点
var marker = new BMap.Marker(point);
// marker.enableDragging(); //小红点不让动
map.addOverlay(marker);
searchInfoWindow.open(marker); //信息窗口 指向marker更好看  可以使用point

console.clear();
console.log("%c", "padding:50px 300px;line-height:120px;background:url('http://pics.sc.chinaz.com/Files/pic/faces/4382/00.gif') no-repeat;");

console.log('%c招聘网站技术人员', 'background-image:-webkit-gradient( linear, left top, right top, color-stop(0, #f22), color-stop(0.15, #f2f), color-stop(0.3, #22f), color-stop(0.45, #2ff), color-stop(0.6, #2f2),color-stop(0.75, #2f2), color-stop(0.9, #ff2), color-stop(1, #f22) );color:transparent;-webkit-background-clip: text;font-size:5em;');
1
console.log("%c有网站开发经验，精通MySQL数据库的应用和开发。。。","text-shadow: 0 1px 0 #ccc,0 2px 0 #c9c9c9,0 3px 0 #bbb,0 4px 0 #b9b9b9,0 5px 0 #aaa,0 6px 1px rgba(0,0,0,.1),0 0 5px rgba(0,0,0,.1),0 1px 3px rgba(0,0,0,.3),0 3px 5px rgba(0,0,0,.2),0 5px 10px rgba(0,0,0,.25),0 10px 10px rgba(0,0,0,.2),0 20px 20px rgba(0,0,0,.15);font-size:3em");

console.log("%c联系方式：15288888888","background: rgba(252,234,187,1);background: -moz-linear-gradient(left, rgba(252,234,187,1) 0%, rgba(175,250,77,1) 12%, rgba(0,247,49,1) 28%, rgba(0,210,247,1) 39%,rgba(0,189,247,1) 51%, rgba(133,108,217,1) 64%, rgba(177,0,247,1) 78%, rgba(247,0,189,1) 87%, rgba(245,22,52,1) 100%);background: -webkit-gradient(left top, right top, color-stop(0%, rgba(252,234,187,1)), color-stop(12%, rgba(175,250,77,1)), color-stop(28%, rgba(0,247,49,1)), color-stop(39%, rgba(0,210,247,1)), color-stop(51%, rgba(0,189,247,1)), color-stop(64%, rgba(133,108,217,1)), color-stop(78%, rgba(177,0,247,1)), color-stop(87%, rgba(247,0,189,1)), color-stop(100%, rgba(245,22,52,1)));background: -webkit-linear-gradient(left, rgba(252,234,187,1) 0%, rgba(175,250,77,1) 12%, rgba(0,247,49,1) 28%, rgba(0,210,247,1) 39%, rgba(0,189,247,1) 51%, rgba(133,108,217,1) 64%, rgba(177,0,247,1) 78%, rgba(247,0,189,1) 87%, rgba(245,22,52,1) 100%);background: -o-linear-gradient(left, rgba(252,234,187,1) 0%, rgba(175,250,77,1) 12%, rgba(0,247,49,1) 28%, rgba(0,210,247,1) 39%, rgba(0,189,247,1) 51%, rgba(133,108,217,1) 64%, rgba(177,0,247,1) 78%, rgba(247,0,189,1) 87%, rgba(245,22,52,1) 100%);background: -ms-linear-gradient(left, rgba(252,234,187,1) 0%, rgba(175,250,77,1) 12%, rgba(0,247,49,1) 28%, rgba(0,210,247,1) 39%, rgba(0,189,247,1) 51%, rgba(133,108,217,1) 64%, rgba(177,0,247,1) 78%, rgba(247,0,189,1) 87%, rgba(245,22,52,1) 100%);background: linear-gradient(to right, rgba(252,234,187,1) 0%, rgba(175,250,77,1) 12%, rgba(0,247,49,1) 28%, rgba(0,210,247,1) 39%, rgba(0,189,247,1) 51%, rgba(133,108,217,1) 64%, rgba(177,0,247,1) 78%, rgba(247,0,189,1) 87%, rgba(245,22,52,1) 100%);filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#fceabb', endColorstr='#f51634', GradientType=1 );font-size:5em");


console.log("我劝天公重抖擞，不拘一格降人才。%c来自:龚自珍","color:red;font-weight:bold;");

</script>
```
