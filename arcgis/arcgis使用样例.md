# 如何使用arcgis

 

## 在esmodules里面使用

```shell
npm install @arcgis/core
```

然后倒入你需要的map

```shell
import Map from "@arcgis/core/Map";
```

注意,和echarts类似,arcgis的视图区域也需要有长宽

```css
#viewDiv {
  padding: 0;
  margin: 0;
  height: 100vh;
  width: 100%;
}
```

## 创建一个简单的地图(MapView 2d)

> 一个简单的vue实例

```vue
<template>
<div class="simple-map"></div>
</template>

<script>
import Map from "@arcgis/core/Map";
import MapView from "@arcgis/core/views/MapView";
import Expand from "@arcgis/core/widgets/Expand";
export default {
  name: "SimpleMap",
  async mounted() {
    const map = new Map({
      basemap: "osm"//这个需要去api看
    });

    const view = new MapView({
      container: this.$el,//你要挂载到该组件的根元素
      map: map,
      zoom: 4,
      center: [117.13168780199648, 31.83669432640482] // 你所在的坐标
    });
    // view.ui.add(map, "top-right");
  }
}
</script>

<style scoped>
@import 'https://cdn.jsdelivr.net/npm/@arcgis/core/assets/esri/css/main.css';
.simple-map{
  padding: 0;
  margin: 0;
  width: 100%;
  height: 100vh;

}
</style>

```

## 创建一个简单的3d地图(sceneView)

```vue
<template>
  <div class="simple-map"></div>
</template>

<script>
import Map from "@arcgis/core/Map";
import SceneView from "@arcgis/core/views/SceneView";
export default {
  name: "SimpleMap",
  async mounted() {
    const map = new Map({
      basemap: "topo-vector",
      ground: "world-elevation",
    });
    const view = new SceneView({
      container: this.$el, //你要挂载到该组件的根元素
      map: map, // References the map object created in step 3
      center: [117.13168780199648, 31.83669432640482],
    });
  },
};
</script>

<style scoped>
@import "https://cdn.jsdelivr.net/npm/@arcgis/core/assets/esri/css/main.css";
.simple-map {
  padding: 0;
  margin: 0;
  width: 100%;
  height: 100vh;
}
</style>

```

## 改变basemapview

```vue
<template>
  <div class="container">
    <div class="simple-map"></div>
  </div>
</template>

<script>
import Map from "@arcgis/core/Map";
import MapView from "@arcgis/core/views/MapView";
import BasemapToggle from "@arcgis/core/widgets/BasemapToggle";
import BasemapGallery from "@arcgis/core/widgets/BasemapGallery";
export default {
  name: "SimpleMap",
  async mounted() {
    const map = new Map({
      basemap: "osm",
    });
    const view = new MapView({
      container: this.$el, //你要挂载到该组件的根元素
      map: map,
      center: [117.13168780199648, 31.83669432640482],
    });
    const basemapToggle = new BasemapToggle({
      view: view,
      nextBasemap: "arcgis-imagery",
    });
    const basemapGallery = new BasemapGallery({
      view: view,
      source: {
        query: {
          title: '"World Basemaps for Developers" AND owner:esri',
        },
      },
    });
    view.ui.add(basemapToggle, "bottom-right");
    view.ui.add(basemapGallery, "top-right");
  },
};
</script>

<style scoped>
@import "https://cdn.jsdelivr.net/npm/@arcgis/core/assets/esri/css/main.css";
.container {
  padding: 0;
  margin: 0;
  width: 100%;
}
.simple-map {
  padding: 0;
  margin: 0;
  width: 100%;
  height: 100vh;
}
</style>

```

## 创建一个弹出层

```vue
<template>
  <div class="container">
    <div class="simple-map"></div>
  </div>
</template>

<script>
import esriConfig from "@arcgis/core/config";
import Map from "@arcgis/core/Map";
import MapView from "@arcgis/core/views/MapView";
import BasemapToggle from "@arcgis/core/widgets/BasemapToggle";
import BasemapGallery from "@arcgis/core/widgets/BasemapGallery";
import VectorTileLayer from "@arcgis/core/layers/VectorTileLayer";
import TileLayer from "@arcgis/core/layers/TileLayer";
import Basemap from "@arcgis/core/Basemap";
export default {
  name: "SimpleMap",
  async mounted() {
    //部分功能可能需要收费,请酌情考虑
    esriConfig.apiKey = "你的apikey";

    const vectorTileLayer = new VectorTileLayer({
      portalItem: {
        id: "6976148c11bd497d8624206f9ee03e30", // Forest and Parks Canvas
      },
      opacity: 0.75,
    });
    const imageTileLayer = new TileLayer({
      portalItem: {
        id: "1b243539f4514b6ba35e7d995890db1d", // World Hillshade
      },
    });
    const basemap = new Basemap({

      baseLayers: [imageTileLayer, vectorTileLayer],
    });
    const map = new Map({
      basemap: basemap,
      zoom: 3,
      center: [117.13168780199648, 31.83669432640482],
    });
    const view = new MapView({
      container: this.$el, //你要挂载到该组件的根元素
      map: map,
      center: [117.13168780199648, 31.83669432640482],
    });
  },
};
</script>

<style scoped>
@import "https://cdn.jsdelivr.net/npm/@arcgis/core/assets/esri/css/main.css";
.container {
  padding: 0;
  margin: 0;
  width: 100%;
}
.simple-map {
  padding: 0;
  margin: 0;
  width: 100%;
  height: 100vh;
}
</style>

```

# 创建可以绘制的图层

```vue
<template>
  <div class="container">
    <div class="simple-sketch"></div>
  </div>
</template>

<script>
import esriConfig from "@arcgis/core/config";
import Map from "@arcgis/core/Map";
import MapView from "@arcgis/core/views/MapView";
import Search from "@arcgis/core/widgets/Search";

import FeatureLayer from "@arcgis/core/layers/FeatureLayer";
import Sketch from "@arcgis/core/widgets/Sketch";
import GraphicsLayer from "@arcgis/core/layers/GraphicsLayer";
export default {
  name: "SimpleSketch",
  async mounted() {
    const graphicsLayer = new GraphicsLayer();
    const map = new Map({
      basemap: "topo-vector",
      layers: [graphicsLayer],
      //Basemap layer service
    });

    const view = new MapView({
      container: this.$el,
      map: map,
      center: [-118.80543, 34.027], //Longitude, latitude
      zoom: 13,
    });

    await view.when(() => {
      const sketch = new Sketch({
        layer: graphicsLayer,
        view: view,
        // graphic will be selected as soon as it is created
        creationMode: "update",
      });

      view.ui.add(sketch, "top-right");
    });
  },
};
</script>

<style scoped>
@import "https://cdn.jsdelivr.net/npm/@arcgis/core/assets/esri/css/main.css";
.container {
  padding: 0;
  margin: 0;
  width: 100%;
}
.simple-sketch {
  padding: 0;
  margin: 0;
  width: 100%;
  height: 100vh;
}
</style>

```

## 如何添加featurelayer

```vue
```

特别注意如何绑定数据     [链接](https://developers.arcgis.com/documentation/mapping-apis-and-services/data-hosting/tutorials/tools/import-data-as-a-feature-layer/)

如果想继续研究,请去官网查看:

官网地址: [链接](https://developers.arcgis.com/documentation/)



如何创建离线地图  [链接](https://developers.arcgis.com/documentation/mapping-apis-and-services/offline/how-to-build-offline-applications/use-data-services-or-files/)

使用argis online [链接](https://developers.arcgis.com/documentation/mapping-apis-and-services/data-hosting/get-started/)
