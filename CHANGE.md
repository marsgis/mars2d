# Mars2D版本及更新日志


# 1. Mars2D的版本

Mars2D的版本号包括三个部分，比如 **v3.2.1**版本中，**主版本号是 3，大版本号是 2，小版本号是 1**

版本号是根据本次发布中包含的变更的级别进行递增的。

- **主版本**(v3)：包含重要的新特性和架构性调整，在升级时会需要由开发人员提供少量的协助才能完成。当升级到新的主版本时，你可能需要运行升级脚本、重构代码、运行其它测试以及学习新的API。

- **大版本**(v3.2)：包含新增功能和API优化重构，大版本其中大部分功能是向后兼容的，只有少部分特性是不兼容的(更新日志会说明弃用的API)，参考说明或示例简单调整即可。

- **小版本**(v3.2.1)：包含新的小型特性优化，bug修改等。 小版本是完全向后兼容的，在升级期间，不需要开发人员提供协助。【授权版时：无论哪种授权方式，小版本均是免费更新】

## 历史版本下载

我们已切换到v3.1.0版本为例：
- npm 安装的项目，请打开package.json修改mars2d版本号`"mars2d": "3.1.0"` ，再npm install重新安装
- 静态引入的，请复制链接[https://registry.npmjs.org/mars2d/-/mars2d-3.1.0.tgz](https://registry.npmjs.org/mars2d/-/mars2d-3.1.0.tgz) 后，在浏览器地址栏粘贴并修改版本号为指定版本后会回车进行下载。

# 2. 发布频率

我们会定期发布新版本，以便随着 Mars2D 的不断演进，你可以提前计划并协调这些升级工作。

> 这些日期仅供一般性参考，如有更改，恕不另行通知。

通常的发布周期如下：
- 主版本 没有时间规划，如果有架构性变化时会升主版本
- 每年 发布1个大版本 
- 每月 发布1个小版本

# 3. 弃用策略
"弃用 & API重构"（比如移除特定的 API 和特性）有时候是必须的，比如创新、更高效率、让最佳实践与时俱进、变更依赖关系甚至来自 Web 平台自身的变化。

要让这些转变尽可能的简单，我们会给你下列保证：
- 我们会尽量减少重大变更的数量，并尽可能提供迁移工具。
- 我们会遵循这里所讲的弃用策略，让你有时间把应用升级到最新的 API 和最佳实践。



# 4. 更新日志
 
## 3.3.4 - 2025-9-20
#### 优化 💪
- 矢量对象增加setOptions方法
- GraphicLayer图层增加loadJSON方法

#### 修复 🔧
- 编辑矢量对象时的编辑点右键菜单未正确获取
- QueryPOI.getAddress方法调用无返回值
- 编辑矢量对象部分情况未触发editStop事件
- 天地图POI服务的offset改为count参数


## 3.3.3 - 2025-8-3 
#### 新增 ⚡
- 新增Rain、Snow、BouncingMarker、PolyDecorator矢量对象
- 增加矢量对象的复制粘贴功能

#### 优化 💪
- Circle增加diffuse样式参数
- Map增加getLayrsTree方法
- 增加mars2d.PolyUtil.movePoints方法
- 增加了一些功能示例（旋转地图、迁徙效果、有线上文本的折线、时序轨迹路线）

#### 修复 🔧
- WmsLayer请求参数去掉冗余的url参数
- FineArrowYW最大点位应该是2个坐标
- AntPath导出JSON有错误
- ArcGisFeatureLayer点图标不显示


## 3.3.2 - 2025-04-20
#### 新增 ⚡
- 新增 BusineDataLayer业务数据图层
- 新增 KeyboardRoam 键盘控制类
- 新增QueryPOI、QueryRoute查询类，内部service参数控制选用天地图、百度、高德服务

#### 优化 💪
- 线面编辑时增加整体平移编辑点
- ClusterLayer增加clusterEnabled属性，可以控制聚合的开关
- QueryGeoServer增加点选查询

#### 弃用 & API重构 🔒
- 移除了TdtPOI、BaiduPOI、GaodePOI、GaodeRoute类(改用QueryPOI、QueryRoute)



## 3.3.1 - 2025-02-06
#### 新增 ⚡
- 新增AntPath矢量对象

#### 优化 💪
- 线面对象增加dashSpeed参数，可以让虚线动起来



## 3.3.0 - 2025-01-23
#### 新增 ⚡
- 线面矢量对象增加dashOffset虚线运动速度参数

#### 优化 💪
- Rectangle、Circle矢量对象toGeoJSON增加outline参数
- 新增AntPath矢量对象到SDK内，方便管理



---
## 3.2.10 - 2024-12-22
#### 修复 🔧
- LocationBar兼容平移全球地图时经度值超过180度
- 矢量对象修改坐标时，部分对象label坐标未同步更新

#### 弃用 & API重构 🔒
- npm包中去掉`dist`子目录，与下载的静态包目录保持一致(如果`import "mars2d/dist/mars2d.css"`报错，请改为`import "mars2d/mars2d.css"`)



## 3.2.6 - 2024-7-5
#### 优化 💪
- 矢量数据标绘时增加右键删除最后一个点位
- control增加show属性
- geojson数据加载支持filter参数筛选数据

#### 修复 🔧
- ArcGisFeatureLayer的symbol配置无效
- Marker的label属性样式相关参数优化
- polyline多色线缩放颜色变化
- 矢量对象附带文本部分情况下未跟随坐标变动



## 3.2.4 - 2024-4-21
#### 优化 💪
- ToolBar优化样式  
- EchartsLayer增加on、off绑定事件
- Marker、Label、DivGraphic增加minZoom、maxZoom限定显示层级参数



## 3.2.1 - 2024-2-22
#### 新增 ⚡
- 矢量对象增加label附加文本属性

#### 优化 💪
- 增加kml、shp格式文件加载示例
- 重写了Util.template方法

#### 修复 🔧
- ClusterLayer聚合图层bindPopup无效



## 3.2.0 - 2024-1-16
#### 新增 ⚡
- 矢量对象增加show属性
- 矢量对象增加hasEdit、isAutoEditing参数



---
## 3.1.25 - 2023-12-31 
#### 修复 🔧
- Polygon.toJSON导出异常
- 瓦片图层show:false传参无效


## 3.1.22 - 2023-10-27 
#### 修复 🔧
- 4490坐标系下天地图显示异常
- ExpImg导出图片未传入回调
- fill和outline部分情况下更新style自动显示了


## 3.1.20 - 2023-9-13
#### 新增 ⚡
- 增加 TdtPOI 查询类

#### 优化 💪
- 矢量对象的zIndex属性支持
- 优化Circle圆的绘制规则

#### 弃用 & API重构 🔒
- 弃用mars3d-widget插件，原生JS技术栈下项目中直接改为使用源码(es5-widget.js)



## 3.1.17 - 2023-7-3
#### 修复 🔧
- graphic和GraphicLayer的pane参数无效
- v3.1.15产生的OverviewMap存在2个矩形框问题
- map的addLayer、removeLayer事件无效



## 3.1.16 - 2023-6-5
#### 新增 ⚡
- 聚合图层增加右键菜单支持
- PointTrans.latlng2coord方法没有高度时不返回0

#### 修复 🔧
- 线面编辑时，外部修改坐标后，图上编辑点未同步修改位置
- 修复v3.1.15产生的ExpImg导出图片出错



## 3.1.15 - 2023-5-23
#### 重要说明 📣
- Leaflet 升级至 [1.9.4](https://github.com/Leaflet/Leaflet/releases/tag/v1.9.4)

#### 新增 ⚡
- GraphicLayer增加bringToBack和bringToFront方法
- Map增加isLoading属性和增加地图加载完成load事件

#### 修复 🔧
- GroupLayer图层zIndex设置无效
- 谷歌在线地图服务修复
- ExpImg.expByDraw按区域截图未恢复地图状态



## 3.1.14 - 2023-4-24
#### 新增 ⚡
- 大部分图层支持透明度设置

#### 修复 🔧
- Marker部分图标定位偏移



## 3.1.12 - 2023-3-20
#### 新增 ⚡
- 新增 SmTileLayer 超图瓦片服务图层



## 3.1.10 - 2023-1-10
#### 重要说明 📣
- Leaflet 升级至 [1.9.3](https://github.com/Leaflet/Leaflet/releases/tag/v1.9.3)

#### 修复 🔧
- 修复mars2d.d.ts错误
- 修复全屏按钮多次切换问题



## 3.1.9 - 2022-11-30
#### 优化 💪
- 量算类增加绘制编辑事件的抛出
- 增加rightClick右键事件
- 矢量数据增加销毁方法

#### 修复 🔧
- 右键菜单绑定地图与矢量数据有叠加
- snake路线多次停止开启运行异常
- 地图scale控件参数无法配置
- MapSplit控件支持数组图层配置


## 3.1.7 - 2022-10-24
#### 重要说明 📣
- Leaflet 升级至 [1.9.2](https://github.com/Leaflet/Leaflet/releases/tag/v1.9.2)

#### 优化 💪
- WfsLayer、ArcGisFeatureLayer等图层增加flyTo方法

#### 修复 🔧
- snakeIn路线style颜色传值无效
- Circle绘制中radius没有动态回传
- formatDate方法格式化无效



## 3.1.6 - 2022-9-16
#### 优化 💪
- vue示例和项目UI部分进行重构
- 矢量数据增加toJSON方法



## 3.1.5 - 2022-8-1
#### 优化 💪
- 对Map中图层内部的存储和读取方式做了优化

#### 弃用 & API重构 🔒
- 图层、矢量数据类弃用uuid属性，全部统一为[id](http://mars2d.cn/api/GraphicLayer.html#id)



## 3.1.4  - 2022-6-26
#### 新增 ⚡
- GeoJsonLayer图层增加chinaCRS参数，支持数据自动纠偏

#### 优化 💪
- vue功能示例编辑器重写
- 增加主库和插件库中第3方依赖JS库未引入时的错误提示，方便排查问题

#### 修复 🔧
- graphicLayer.openPopup偶尔报错问题
- GeoJsonLayer图层popupOptions参数未生效



## 3.1.3  - 2022-4-29
#### 重要说明 📣
- Leaflet 升级至 [1.8.0](https://github.com/Leaflet/Leaflet/releases/tag/v1.8.0)
- 发布了 v3.1 版
- SDK内部重新架构

#### 新增 ⚡
- 增加MapSplit双屏对比控件
- 更新mars2d.Token所有默认值
- 增加mars2d.Token.updateAll方法，方便外部更新覆盖

#### 修复 🔧
- 修复部分DivGraphic拖拽后的定位存在偏差
- 修复一些已知bug

 

## 3.0.9  - 2022-3-8
#### 新增 ⚡
- Circle增加outlineLatlngs属性
- 增加QueryArcServer、QueryGeoServer查询类
- 新增了一批示例

#### 修复 🔧
- 自由线绘制的偶尔报错
- 量算的编辑
- GaodePOI 中限定区域无效



## 3.0.8  - 2022-2-25
#### 重要说明 📣
- 基础项目vue版上线发布
- 功能示例原生JS版优化(与Vue版保持一致性)

#### 新增 ⚡
- 增加ToolButton控件
- 完善API文档及TS定义


 
## 3.0.7  - 2022-2-20
#### 重要说明 📣
- 功能示例vue版上线发布
 
#### 新增 ⚡
- wms图层增加click事件和popup支持
- 增加ToolButton控件
- 增加 mars2d.d.ts 对TS支持

#### 修复 🔧
- 检查API文档描述错误并修复
- 修复v3.0.5版show修改带来的瓦片图层不展示
- 圆、矩形完成后激活编辑失败 
- 测试了一轮并修复了一批bug问题

#### 弃用 & API重构 🔒
- 移除axios库，改用 mars2d.Util.fetchJson或sendAjax方法
- 优化pbf图层，vectorTileLayerStyles参数改名style，并简化了参数形式


## 3.0.5  - 2022-1-17
#### 优化 💪
- 对图层增加show参数和属性
- 优化状态栏的小分辨率时的显示

#### 修复 🔧
- 修复已知的一些bug

 

## 3.0.3  - 2021-12-17
#### 重要说明 📣
- Leaflet 升级至 [1.7.1](https://github.com/Leaflet/Leaflet/releases/tag/v1.7.1)
- 完成所有 V2 的功能示例的对应 V3 新版开发
- v3.0正式稳定版本发布
- 优化了SDK内部的接口方法，并整理及发布API文档
- 完成了教程的编写

#### 修复 🔧
- 完成了一轮测试并修复了所有bug问题

 


## 3.0.0  - 2021-11-16
#### 重要说明 📣
- 发布了 v3.0 版
- 易学：使用和语法都按开发人员用户习惯最优设计，降低开发人员能力要求，只用初级水平开发人员即可上手。
- 规范：API 从顶层统一规范的从零重构、将插件优化至SDK内，并提供统一规范的API。
- 高效率：提高了开发效率和平台的渲染效率。
- 详细的 API 和教程：重新编写了详细的教程文档、自动根据 SDK 注释生成的最详尽的 API 文档，并完全免费开放。
- 功能示例和项目模板：并规划开发了 Vue 版 功能示例和基础项目。
- 免费：免费无限制使用

#### 新增 ⚡
- 矢量数据：全新设计了矢量数据体系，采用Graphic矢量数据（统一的规范和style设计）和GraphicLayer矢量数据图层来统一管理。
- GeoJson图层：设计了新的GeoJsonLayer，采用可在symobl中配置type参数指定Graphic类型来渲染。

#### 弃用 & API重构 🔒
- v3.0版与v2.x版本还不兼容(API结构不同)，无法兼容平滑的升级，因为v3所有代码从零开始编写搭建的,不是基于之前的老版本修改的。
 

---

## 2.0.0  - 2020-1-1
#### 重要说明 📣
- 发布了v2.0



## 1.0.0  - 2017-8-25
#### 重要说明 📣
- 发布了v1.0
