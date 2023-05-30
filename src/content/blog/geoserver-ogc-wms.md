---
title: Geoserver Services-WMS
description: OGC规范-WMS (Web Map Service)
pubDatetime: 2023-05-30T17:10:05.274+08:00
postSlug: geoserver-ogc-wms
featured: false
tags:
  - geoserver
---

> https://docs.geoserver.org/stable/en/user/services/wms/reference.html

#### Table of content

## 不同版本的区别

1. 坐标系统顺序不一样，1.1.0 的顺序是经度/纬度，而 1.3.0 的顺序是纬度/经度
2. 坐标系参数从 1.1.0 srs 转到 1.3.0 crs

```shell
# 1.1.0
geoserver/wms?VERSION=1.1.1&REQUEST=GetMap&SRS=epsg:4326&BBOX=-180,-90,180,90&…
# 1.3.0
geoserver/wms?VERSION=1.3.0&REQUEST=GetMap&CRS=epsg:4326&BBOX=-90,-180,90,180&…
```

## 功能

| 操作             | 描述                                                           |
| ---------------- | -------------------------------------------------------------- |
| GetCapabilities  | 获取有关服务的元数据，包括支持的操作和参数，以及可用图层的列表 |
| GetMap           | 获取指定区域和内容的地图图像                                   |
| GetFeatureInfo   | 获取地图上像素位置的基础数据，包括几何和属性值                 |
| DescribeLayer    | 指示 WFS 或 WCS 以检索有关图层的附加信息                       |
| GetLegendGraphic | 获取地图的生成图例                                             |

### GetCapabilities

```shell
http://localhost:8080/geoserver/wms?
service=wms&
version=1.1.1&
request=GetCapabilities
```

### GetMap

```shell
http://localhost:8080/geoserver/wms?
request=GetMap
&service=WMS
&version=1.1.1
&layers=topp%3Astates
&styles=population
&srs=EPSG%3A4326
&bbox=-145.15104058007,21.731919794922,-57.154894212888,58.961058642578&
&width=780
&height=330
&format=image%2Fpng
```

### GetFeatureInfo

```shell
http://localhost:8080/geoserver/wms?
&INFO_FORMAT=application/json
&REQUEST=GetFeatureInfo
&EXCEPTIONS=application/vnd.ogc.se_xml
&SERVICE=WMS
&VERSION=1.1.1
&WIDTH=970&HEIGHT=485&X=486&Y=165&BBOX=-180,-90,180,90
&LAYERS=COUNTRYPROFILES:grp_administrative_map
&QUERY_LAYERS=COUNTRYPROFILES:grp_administrative_map
&TYPENAME=COUNTRYPROFILES:grp_administrative_map
```

### DescribeLayer

```shell
http://localhost:8080/geoserver/wms?service=WMS
&version=1.1.1
&request=DescribeLayer
&layers=sf:roads,topp:tasmania_roads,nurc:mosaic
&outputFormat=application/json
```

### GetLegendGraphic
