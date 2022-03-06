# Mars2D更新日志  

------------------------------------------- 
## 3.0.9  - 2022-3-6
#### Additions 🎉
- Circle增加outlineLatlngs属性
- 增加QueryArcServer、QueryGeoServer查询类

#### Fixes 🔧  
- 自由线绘制的偶尔报错
- 量算的编辑
- GaodePOI 中限定区域无效



## 3.0.8  - 2022-2-25
#### Breaking Changes 📣
- 基础项目vue版上线发布

#### Additions 🎉
- 增加ToolButton控件
- 完善API文档及TS定义


 
## 3.0.7  - 2022-2-20
#### Breaking Changes 📣
- 功能示例vue版上线发布
- 移除axios库，改用 mars2d.Util.fetchJson或sendAjax方法
- 优化pbf图层，vectorTileLayerStyles参数改名style，并简化了参数形式

#### Additions 🎉 
- wms图层增加click事件和popup支持
- 增加ToolButton控件
- 增加 mars2d.d.ts 对TS支持 (测试中,可能有问题)

#### Fixes 🔧  
- 检查API文档描述错误并修复
- 修复v3.0.5版show修改带来的瓦片图层不展示
- 圆、矩形完成后激活编辑失败 
- 测试了一轮并修复了一批bug问题



## 3.0.5  - 2022-1-17
#### Additions 🎉
- 对图层增加show参数和属性
- 优化状态栏的小分辨率时的显示

#### Fixes 🔧  
- 修复已知的一些bug

 

## 3.0.3  - 2021-12-17
#### Breaking Changes 📣
- v3.0正式稳定版本发布
- 完成了教程的编写

#### Fixes 🔧  
- 完成了一轮测试并修复了所有bug问题


## 3.0.1  - 2021-12-14
#### Breaking Changes 📣
- 优化了SDK内部的接口方法，并整理及发布API文档
- 完成了教程的初步编写
- 增加了一批新的示例
 

 
## 3.0.0  - 2021-11-16
#### Breaking Changes 📣
- 发布了v3第一个测试版本。

#### Additions 🎉 
- 按“规范、高效率、易学易用”为准则架构，从零开始重构开发的v3.0新版本，并开放开源免费使用。
- 全新设计了矢量数据体系，采用Graphic矢量数据（统一的规范和style设计）和GraphicLayer矢量数据图层来统一管理。
- 设计了新的GeoJsonLayer，采用可在symobl中配置type参数指定Graphic类型来渲染。


-------------------------------------------

## 2.0.0  - 2020-1-1
#### Breaking Changes 📣
- 发布了v2.0


## 1.0.0  - 2017-8-25
#### Breaking Changes 📣
- 发布了v1.0
