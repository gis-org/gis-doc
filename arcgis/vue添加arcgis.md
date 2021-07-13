# vue中使用arcgis

## 在vue中安装ArcGis

vue中使用arcgis很简单,你可以使用下面三种地图依赖



```shell
@arcgis/core arcgis核心
ol           openlayer核心
mapbox-gl    mapbox核心

```

> 安装依赖命令如下

```shell
yarn add @arcgis/core
yanr add ol
yarn add mabox-gl
```

>  注意: 下面的教程对于 **v4.18**版本以下有效,对**v4.18**以上我推荐使用直接引入`@arcgis/core`这个包

**如果低于v4.18版本 ** 

在vue中使用arcgis需要一个叫做**esri-loader**的东西来帮我们加载arcgis文件。

```javascript
yarn add esri-loader  
```

npm上的相关文档参考：[https://www.npmjs.com/package/esri-loader](https://www.npmjs.com/package/esri-loader)

首先在你的vue组件中引入esri-loader

```javascript
import esriLoader from  'esri-loader'
```

样式文件可以在main.js中引入，也可以在当前组件引入，我选择的是在main.js中引

```javascript
import '@arcgis/core/assets/esri/css/main.css' 
```

最后加载就可以使用arcgis的api了，部分代码如下

```js
 import { loadModules } from 'esri-loader';

// this will lazy load the ArcGIS API
// and then use Dojo's loader to require the classes
loadModules(['esri/views/MapView', 'esri/WebMap'])
  .then(([MapView, WebMap]) => {
    // then we load a web map from an id
    var webmap = new WebMap({
      portalItem: { // autocasts as new PortalItem()
        id: 'f2e9b762544945f390ca4ac3671cfa72'
      }
    });
    // and we show that map in a container w/ id #viewDiv
    var view = new MapView({
      map: webmap,
      container: 'viewDiv'
    });
    console.log(webmap)
  })
  .catch(err => {
    // handle any errors
    console.error(err);
  });
```

如果没有报错,并且成功打印map就说明可以使用了

 