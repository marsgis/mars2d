# Mars2D 版本及更新日志

## 1. Mars2D 的版本

Mars2D 的版本号由三段组成。以 **v3.2.1** 为例：**主版本号为 3，大版本号为 2，小版本号为 1**。

版本号按本次发布所包含变更的级别递增。

- **主版本**（v3）：包含重要新特性与架构性调整，升级时可能需要开发人员少量配合。升级到新的主版本时，可能需要执行升级脚本、重构代码、补充测试并学习新的 API。
- **大版本**（v3.2）：包含新增功能与 API 优化重构。大部分功能向后兼容，仅少数特性不兼容（更新日志会说明弃用的 API），参照说明或示例做简单调整即可。
- **小版本**（v3.2.1）：包含小幅特性优化与缺陷修复等，完全向后兼容，升级期间无需开发人员配合。授权版无论采用哪种授权方式，小版本均可免费更新。

## 历史版本下载

以 v3.1.0 版本为例：
- npm 安装的项目：打开 package.json，把 mars2d 的版本号改为 `"mars2d": "3.1.0"`，再执行 `npm install` 重新安装。
- 静态引入的项目：复制链接 [https://registry.npmjs.org/mars2d/-/mars2d-3.1.0.tgz](https://registry.npmjs.org/mars2d/-/mars2d-3.1.0.tgz)，在浏览器地址栏粘贴后把版本号改成目标版本，回车即可下载。

## 2. 发布频率

我们会定期发布新版本，你可以据此提前规划并安排升级工作。

> 以下时间仅供参考，如有调整不再另行通知。

通常的发布周期如下：
- 主版本：无固定周期，出现架构性变化时升级。
- 大版本：每年发布 1 个。
- 小版本：每月发布 1 个。

## 3. 弃用策略

“弃用与 API 重构”（例如移除某个 API 或特性）有时不可避免：为了创新、提升效率、跟上最佳实践、调整依赖关系，甚至应对 Web 平台自身的变化。

为让这些转变尽可能平滑，我们给出以下保证：
- 尽量减少破坏性变更，并尽可能提供迁移工具。
- 遵循本策略，为应用升级到最新 API 和最佳实践留出时间。

## 4. 更新日志

## 3.5.1 - 2026-11-07

#### 新增 ⚡
- 新增 [CanvasMarkerLayer.getContext()](http://mars2d.cn/api/CanvasMarkerLayer.html#getContext)，在 customDraw 回调中可直接获取 Canvas 2D 上下文绘制个性点，画布未初始化时返回 null（示例：[CanvesMarker大数据点图层](http://mars2d.cn/editor-vue.html?id=layer-graphic/basis/canvas-marker)）。
- 新增 [FeatureGroup.getLatLngs()](http://mars2d.cn/api/FeatureGroup.html#getLatLngs)，按成员聚合返回经纬度数组，组合矢量对象可直接读取整体坐标。
- 新增 [CanvasImage.getLatLngs()](http://mars2d.cn/api/CanvasImage.html#getLatLngs)，返回图片矩形的四角坐标（示例：[CanvasImage 图片](http://mars2d.cn/editor-vue.html?id=graphic/basis/image-canvas)）。

#### 优化 💪
- 工程：新增 API 冒烟测试与多项回归测试，端到端覆盖率与单元覆盖率合并统计，CI 串联 lint、构建、声明校验、单元测试与 E2E。
- WFS：`loadFeatures` 支持传入多个过滤条件（数组按 And 组合）；请求带代际标记，切换图层或清空后旧响应不再写入；`show:false` 或缩放层级不满足时不再请求与渲染要素（示例：[OGC WFS服务](http://mars2d.cn/editor-vue.html?id=layer-graphic/wfs/ogc-wfs)）。
- PBF：重写瓦片渲染生命周期，瓦片卸载时释放渲染器与事件，图片异步加载完成后按需重绘，缩放与平移后不再出现空白瓦片（示例：[pbf矢量瓦片服务](http://mars2d.cn/editor-vue.html?id=layer-graphic/wfs/pbf)）。
- 雨雪：[Rain](http://mars2d.cn/api/Rain.html) 的顶点数据改为一次构建与写入，着色器编译后及时释放，移除时释放 program 与缓冲，降低大量粒子场景下的内存占用（示例：[雪](http://mars2d.cn/editor-vue.html?id=graphic/basis/snow)）。

#### 修复 🔧
- [Map](http://mars2d.cn/api/Map.html)：[addLayer](http://mars2d.cn/api/Map.html#addLayer) 重复添加同一图层时直接返回已有对象；[removeLayer](http://mars2d.cn/api/Map.html#removeLayer) 移除未上图图层时安全返回；图层 id 为 0，或字符串与数字形式的同一 id 冲突时不再被重新赋值；[getNextLayerId](http://mars2d.cn/api/Map.html#getNextLayerId) 不再返回已占用的 id。
- [Map](http://mars2d.cn/api/Map.html)：[getLayersByAttr](http://mars2d.cn/api/Map.html#getLayersByAttr) 合并配置图层并去重；[removeLayers](http://mars2d.cn/api/Map.html#removeLayers) 与内部图层列表、removeLayer 事件保持一致；[removeControl](http://mars2d.cn/api/Map.html#removeControl) 只清理当前控件对应的缓存。
- [Map](http://mars2d.cn/api/Map.html)：[remove()](http://mars2d.cn/api/Map.html#remove) 会清理 Thing、图层计时器、SmallTooltip、右键菜单与水印容器；[addThing](http://mars2d.cn/api/Map.html#addThing)、[removeThing](http://mars2d.cn/api/Map.html#removeThing)、[hasThing](http://mars2d.cn/api/Map.html#hasThing) 按实例判重，`_onAdd` 抛错时回滚登记。
- [Map](http://mars2d.cn/api/Map.html)：[setOptions](http://mars2d.cn/api/Map.html#setOptions) 的 crs、center、zoom、maxBounds、右键菜单与滚轮缩放按新值生效，不再重复绑定默认菜单；同时配置 center 与 extent 时 [flyHome](http://mars2d.cn/api/Map.html#flyHome) 优先定位 extent；`basemap` 只加载目标底图。
- [GraphicLayer](http://mars2d.cn/api/GraphicLayer.html)：图层 show 与单个 graphic 的 show 正确联动；重复添加同一矢量对象不再重复上图；支持按 id 移除矢量对象；[getGraphicById](http://mars2d.cn/api/GraphicLayer.html#getGraphicById) 支持 id 为 0；[clearLayers](http://mars2d.cn/api/GraphicLayer.html#clearLayers) 会先停止编辑，[loadJSON](http://mars2d.cn/api/GraphicLayer.html#loadJSON) 未挂图时不再报错。
- [GraphicLayer](http://mars2d.cn/api/GraphicLayer.html) 绘制：[startDraw](http://mars2d.cn/api/GraphicLayer.html#startDraw) 返回的 Promise 在取消、清空或重复结束时返回 null 而不再挂起；[endDraw](http://mars2d.cn/api/GraphicLayer.html#endDraw)、[stopDraw](http://mars2d.cn/api/GraphicLayer.html#stopDraw)、[clearDrawing](http://mars2d.cn/api/GraphicLayer.html#clearDrawing) 统一销毁绘制对象并解绑事件，连续标绘可正常进入下一次（示例：[标绘](http://mars2d.cn/editor-vue.html?id=layer-graphic/draw/draw)）。
- [CanvasMarkerLayer](http://mars2d.cn/api/CanvasMarkerLayer.html)：未上图时先添加数据、移除后重新添加、移除图标时不再出现空引用错误，重新挂载后画布正常重绘（示例：[CanvesMarker大数据点图层](http://mars2d.cn/editor-vue.html?id=layer-graphic/basis/canvas-marker)）。
- [Marker](http://mars2d.cn/api/Marker.html)：移除后解绑 zoom 监听，避免重复添加时监听累积；[setStyle](http://mars2d.cn/api/Marker.html#setStyle) 未提供图标来源时保留原图标而不再崩溃（示例：[Marker 图标点](http://mars2d.cn/editor-vue.html?id=graphic/basis/marker)）。
- [AntPath](http://mars2d.cn/api/AntPath.html)：移除后再次添加可正常显示；addLatLng、setLatLngs 后内部坐标与两条子线保持同步（示例：[动画效果线](http://mars2d.cn/editor-vue.html?id=graphic/basis/antpath)）。
- [PolyDecorator](http://mars2d.cn/api/PolyDecorator.html)：未挂图即可读取 [getLatLngs](http://mars2d.cn/api/PolyDecorator.html#getLatLngs)、bounds 与导出；style 未配置 symbol 时按普通线处理而不再崩溃（示例：[线面装饰点](http://mars2d.cn/editor-vue.html?id=graphic/basis/polyDecorator)）。
- [Polygon.isInPoly](http://mars2d.cn/api/Polygon.html#isInPoly) 支持多面与带洞面的判断；线上文本的鼠标事件改为派发带 originalEvent 的矢量事件，与线本身保持一致（示例：[Polygon 面](http://mars2d.cn/editor-vue.html?id=graphic/basis/polygon)）。
- [Image](http://mars2d.cn/api/Image.html) 与 [CanvasImage](http://mars2d.cn/api/CanvasImage.html)：setStyle 修改 url 后图片立即更新；CanvasImage 补齐 getLatLngs 并修正 toGeoJSON，导出不再报错（示例：[CanvasImage 图片](http://mars2d.cn/editor-vue.html?id=graphic/basis/image-canvas)）。
- [Rain](http://mars2d.cn/api/Rain.html)、[Snow](http://mars2d.cn/api/Snow.html)：WebGL 不可用或图层移除后 setStyle、drawScene、redraw 不再空引用崩溃，重新添加可继续渲染（示例：[雨](http://mars2d.cn/editor-vue.html?id=graphic/basis/rain)、[雪](http://mars2d.cn/editor-vue.html?id=graphic/basis/snow)）。
- 绘制与编辑：撤销临时点、取消绘制后的延迟触发不再误完成；自由线首段从起点开始；圆、矩形在拖动结束前已取消时不再触发完成；[EditEllipse](http://mars2d.cn/api/EditEllipse.html) 缩放手柄跟随椭圆旋转角度；[EditPoly](http://mars2d.cn/api/EditPoly.html) 连续越界提示后恢复原颜色（示例：[标绘](http://mars2d.cn/editor-vue.html?id=layer-graphic/draw/draw)）。
- 控件：[MapSplit](http://mars2d.cn/api/MapSplit.html) 多个实例不再共用拖拽状态；[Slider](http://mars2d.cn/api/Slider.html) 修正最小层级下的起始值、释放 document 鼠标事件、minZoom 等于 maxZoom 时不再除零；[ToolBar](http://mars2d.cn/api/ToolBar.html) 支持 zoom 为 0 并清理定位图标；[SmallTooltip](http://mars2d.cn/api/SmallTooltip.html) 坐标为 0 时不再被当作未传（示例：[卷帘对比](http://mars2d.cn/editor-vue.html?id=control/basis/mapSplit)、[鱼骨导航](http://mars2d.cn/editor-vue.html?id=control/basis/slider)）。
- 矢量图层：[GeoJsonLayer](http://mars2d.cn/api/GeoJsonLayer.html) 的 mask 支持 MultiPolygon 与多要素，数据未加载时 [getBounds](http://mars2d.cn/api/GeoJsonLayer.html#getBounds) 不再取错范围；[BusineDataLayer](http://mars2d.cn/api/BusineDataLayer.html) 初始 show:false 时在显示后加载；[ClusterLayer](http://mars2d.cn/api/ClusterLayer.html) 重复添加与未上图添加安全（示例：[绘制反选遮罩层](http://mars2d.cn/editor-vue.html?id=layer-tile/manage/mask)、[聚合点 图层](http://mars2d.cn/editor-vue.html?id=layer-graphic/basis/cluster)）。
- 矢量图层：[GroupLayer](http://mars2d.cn/api/GroupLayer.html) 的 length 返回实际图层数；[GraticuleLayer](http://mars2d.cn/api/GraticuleLayer.html) 经纬度为 0 或画布未初始化时不再漏绘、报错；[HeatLayer](http://mars2d.cn/api/HeatLayer.html) 移除时取消动画帧（示例：[经纬网](http://mars2d.cn/editor-vue.html?id=layer-graphic/other/graticule)、[热力图](http://mars2d.cn/editor-vue.html?id=layer-other/heatLayer)）。
- 瓦片图层：[WmsLayer](http://mars2d.cn/api/WmsLayer.html)、[WmtsLayer](http://mars2d.cn/api/WmtsLayer.html) 的查询结果在图层移除或隐藏后不再弹窗；[ArcGisCompactLayer](http://mars2d.cn/api/ArcGisCompactLayer.html) 索引或瓦片解析失败时结束瓦片加载；[MapboxLayer](http://mars2d.cn/api/MapboxLayer.html) 的 scaleFactor 为 false 时不再拼接 @2x；[SmTileLayer](http://mars2d.cn/api/SmTileLayer.html) 使用实际瓦片尺寸计算分辨率；[TileLayer](http://mars2d.cn/api/TileLayer.html) 的 customColor 在 setOptions 后生效，缩略图缓存失败会释放。
- 查询：[QueryPOI](http://mars2d.cn/api/QueryPOI.html) 的 [autoTip](http://mars2d.cn/api/QueryPOI.html#autoTip) 接受经纬度并正确转换，范围查询的 polygon 经纬度顺序修正；百度矩形范围补齐四角，高德多边形首尾闭合；天地图单条路线与 extent 为 0 的情况不再报错；[QueryGeoServer](http://mars2d.cn/api/QueryGeoServer.html) 空响应转为失败回调（示例：[POI点查询](http://mars2d.cn/editor-vue.html?id=query/poi)）。
- 插件：[ArcGisDynamicLayer](http://mars2d.cn/api/ArcGisDynamicLayer.html) 移除后解绑地图 click、dblclick 与延时回调，弹窗关闭时不再清理已销毁的高亮图层（示例：[ArcGIS MapServer动态服务](http://mars2d.cn/editor-vue.html?id=layer-graphic/wfs/arcgis-dynamic)）。
- 其它：请求 data 为 0 或空字符串时不再被丢弃，且不修改调用方传入的 headers；全屏能力检测、进入与退出兼容更多浏览器，失败时不再抛出未捕获异常；Proj.GeoJSON 解析嵌套要素时保留 crs 转换并回填坐标高度；右键连续粘贴不再修改剪贴板对象；[FeatureGroup](http://mars2d.cn/api/FeatureGroup.html) 克隆、无坐标面要素比较、两点以下的偏移线不再报错（示例：[右键菜单](http://mars2d.cn/editor-vue.html?id=control/inside/contextmenu)）。

## 3.5.0 - 2026-11-01
#### 重要说明 📣
- 优化 SDK 打包：主文件 mars2d.js大小减小了约60%，同时提升运行性能。
- 梳理 mars2d.d.ts 类型声明，补齐与运行时一致的公开成员。
- 全面校正 JSDoc 注释与实际实现不一致的问题（默认值、返回值、继承关系、失效选项等），并删除或标注尚未实现的选项与文档占位。API文档支持查询属性、方法名称，并修复子类未正常显示继承于父类相关方法的错误。
- 新增自动化测试体系：单元、契约与示例驱动测试, 真实 Chrome/Edge 端到端测试）、c8 覆盖率门槛、采集浏览器覆盖率并与 c8 合并, 串联静态检查 → 构建 → 声明校验 → 单测 → E2E。

#### 新增 ⚡
- 新增 [Map.removeLayers()](http://mars2d.cn/api/Map.html#removeLayers)，一次移除多个图层：结果与逐个调用 [removeLayer()](http://mars2d.cn/api/Map.html#removeLayer) 一致（同样触发 removeLayer 事件并同步图层管理控件），但内部图层列表只做一次批量清理；批量移除 5000 个图层由约 36ms 降到约 9ms（Node 24 + jsdom 基准）。
- 新增 [MarsArray.removeMany()](http://mars2d.cn/api/MarsArray.html#removeMany)，按主键批量删除并保留其余元素顺序，避免逐个 [remove()](http://mars2d.cn/api/MarsArray.html#remove) 的 O(n²)；5000 条删除由约 27ms 降到约 1ms（口径同上）。

#### 优化 💪
- SVG 渲染：图片填充 pattern 按「图片 + 颜色 + 透明度」复用，避免每次 setStyle 新增节点导致 defs 无限增长；fillOpacity、imageOpacity 为 0 时不再被当作 1。
- [GraphicLayer.clear()](http://mars2d.cn/api/GraphicLayer.html#clear) 改为批量清理，避免大数据量下逐个移除带来的 O(n²) 开销。
- 标绘算法：闭合曲面、集结地的 normals 累加改用 push；GeoJSON 批量转换避免循环 concat；斜面标绘去掉每帧重复的 setStyle。
- 其它：导出下载后释放 Blob URL；复用右键菜单尺寸缓存；[Marker](http://mars2d.cn/api/Marker.html) 图标尺寸轮询增加超时上限。
- [Map.addLayer](http://mars2d.cn/api/Map.html#addLayer)：不再把 Leaflet 内部渲染器（L.SVG、L.Canvas）登记为图层，[getLayers()](http://mars2d.cn/api/Map.html#getLayers)、[getLayrsTree()](http://mars2d.cn/api/Map.html#getLayrsTree)、[getLayersByAttr()](http://mars2d.cn/api/Map.html#getLayersByAttr) 不再返回内部对象；外部传入且没有 id 的原生 Leaflet 图层会自动按 [getNextLayerId()](http://mars2d.cn/api/Map.html#getNextLayerId) 赋值，避免多个无 id 图层在图层列表中相互覆盖。
- 依赖：运行时升级至 ECharts 6、pbf 5、rbush 4、@mapbox/vector-tile 3、simpleheat 1、proj4 2.22、esri-leaflet 3.0.19、@terraformer/arcgis 2.2.2；[PbfLayer](http://mars2d.cn/api/PbfLayer.html) 适配 PbfReader，[HeatLayer](http://mars2d.cn/api/HeatLayer.html) 适配 SimpleHeat 的构造方式；`mars2d` 自引用移入 devDependencies。
- 构建：Rollup 2 升级至 Rollup 4，保持原有产物语义；消除 mars2d-esri 插件的 `Illegal reassignment to import` 告警；构建与打包脚本适配 commander 15、chalk 6、glob 14 的新入口。
- 工程：d.ts 生成链路改用 TS AST，把字符串枚举改写为 `declare const` + `declare type`，把「其他」「其他参数」占位属性改写为索引签名，并新增声明校验脚本。
- 坐标转换：[PointTrans.proj4Trans()](http://mars2d.cn/api/PointTrans.html#.proj4Trans) 按坐标系对缓存 proj4 转换器，不再逐点重建投影对象；2 万个坐标点做 EPSG:4527→4326 转换由约 73ms 降到约 24ms（约 65%，Node 24 + jsdom 基准）。
- 样式转换：[BaseStyleConver](http://mars2d.cn/api/BaseStyleConver.html) 的排除键表改为常量，不再按样式键逐个新建数组；2 万次转换由约 20ms 降到约 6ms（约 68%，口径同上）。
- 鼠标交互：[Map.setCursor()](http://mars2d.cn/api/Map.html#setCursor) 与 [SmallTooltip.close()](http://mars2d.cn/api/SmallTooltip.html#close) 在样式值未变化时跳过 DOM 写入，鼠标快速扫过 [CanvasMarkerLayer](http://mars2d.cn/api/CanvasMarkerLayer.html) 时不再反复触发样式失效；10 万次 setCursor 由约 260ms 降到约 47ms（约 82%，口径同上）。
- 点位批量：[CanvasMarkerLayer.addGraphics()](http://mars2d.cn/api/CanvasMarkerLayer.html#addGraphics) 整批只取一次地图范围，2 万个标记由约 40ms 降到约 22ms（约 45%，口径同上）（示例：[CanvesMarker大数据点图层](http://mars2d.cn/editor-vue.html?id=layer-graphic/basis/canvas-marker)）。
- WFS：[WfsLayer](http://mars2d.cn/api/WfsLayer.html) 改用集合记录已加载要素与分块缓存，不再逐要素线性查找（O(n²) → O(n)）（示例：[OGC WFS服务](http://mars2d.cn/editor-vue.html?id=layer-graphic/wfs/ogc-wfs)）。
- 经纬网：[GraticuleLayer](http://mars2d.cn/api/GraticuleLayer.html) 同一次视图变化只重绘一次，画布尺寸未变化时不再重置 canvas 后备存储（示例：[经纬网](http://mars2d.cn/editor-vue.html?id=layer-graphic/other/graticule)）。
- 其它细节：矢量对象加入/移出地图与 setStyle 时不再创建一次性闭包；[Map.getNextLayerId()](http://mars2d.cn/api/Map.html#getNextLayerId) 的已占用 id 集合改用 Set；[Util.template()](http://mars2d.cn/api/Util.html#.template) 去掉前置的整串正则 test。
- 构建：私有成员改名逻辑集中到 scripts/build/private-property/，新增白名单 config.js 与兄弟项目使用快照 snapshot.json，压缩产物中被下游继承或覆盖的私有成员名保持稳定。
- 文档：[Map](http://mars2d.cn/api/Map.html) 的 renderer 参数说明与 [GraphicLayer](http://mars2d.cn/api/GraphicLayer.html) 类注释补充大数据量下的渲染器选择与实测结论（2 万面要素改用 renderer: L.canvas() 后首屏约 0.3s、拖拽约 59fps；默认 SVG 下 5000 面即降到约 4fps），并补充 graphicOptions 参数说明（示例：[GeoJson大数据面(Canvas合并渲染)](http://mars2d.cn/editor-vue.html?id=layer-graphic/file/geojson-canvas)）。

---

## 3.4.4 - 2026-10-31
#### 修复 🔧
- [Circle](http://mars2d.cn/api/Circle.html) 轮廓坐标计算：角度单位由「度」改为「弧度」，并按纬度修正墨卡托半径，修复 [outlineLatlngs](http://mars2d.cn/api/Circle.html#outlineLatlngs) 与圆形查询范围错误。
- [Map](http://mars2d.cn/api/Map.html)：[getThing](http://mars2d.cn/api/Map.html#getThing) 返回查询到的 Thing；[isFullscreen](http://mars2d.cn/api/Map.html#isFullscreen) 返回真实全屏状态；[addLayer](http://mars2d.cn/api/Map.html#addLayer) 返回图层对象；[setOptions](http://mars2d.cn/api/Map.html#setOptions) 支持字符串形式的 crs；getGraphicById 修正 attr 拼写。
- [Map](http://mars2d.cn/api/Map.html)：[bounds](http://mars2d.cn/api/Map.html#bounds) 的 setter 改用 fitBounds（Leaflet 没有 setBounds）；[destroy()](http://mars2d.cn/api/Map.html#destroy) 幂等，销毁后 [removeLayer](http://mars2d.cn/api/Map.html#removeLayer) 安全返回；[getLayersByAttr](http://mars2d.cn/api/Map.html#getLayersByAttr) 未命中时不再混入 null、undefined。
- [AntPath](http://mars2d.cn/api/AntPath.html)：修正 [toGeoJSON](http://mars2d.cn/api/AntPath.html#toGeoJSON) 的精度参数（此前导出的坐标全为 NaN）；修正绘制类型判断。
- 测量标绘：距离、面积在单点取消或撤销顶点时不再抛出异常，返回的 Promise 不再永久挂起；按 Esc 取消后不再产生半成品，返回 null（示例：[量算](http://mars2d.cn/editor-vue.html?id=thing/measure)）。
- 编辑：图形未上图时，isAutoEditing 延迟到 add 之后再创建编辑点，避免构造期崩溃与 disable 报错。
- 绘制：取消绘制（按 Esc 或再次点击）时，[BaseDraw](http://mars2d.cn/api/BaseDraw.html) 同步向图层派发 drawCancel，[GraphicLayer.startDraw()](http://mars2d.cn/api/GraphicLayer.html#startDraw) 返回的 Promise 不再永久挂起（示例：[标绘](http://mars2d.cn/editor-vue.html?id=layer-graphic/draw/draw)）。
- 图形基类：setOptions 局部更新时不再错误地解除 popup、tooltip 与右键菜单的绑定；未上图时设置 label 不再崩溃；toJSON 对纯 Leaflet 图层（无 marsOptions）做兜底，不再误判为「GML 解析器不可用」。
- 控件：[ToolBar](http://mars2d.cn/api/ToolBar.html) 的 bbox 分支不再被后续 setView 覆盖，定位定时器在移除时清理；修复 [MapSwich](http://mars2d.cn/api/MapSwich.html) 的高亮问题；[Slider](http://mars2d.cn/api/Slider.html) 释放 document 上的鼠标事件；[OverviewMap](http://mars2d.cn/api/OverviewMap.html) 移除时销毁 miniMap（示例：[工具按钮栏](http://mars2d.cn/editor-vue.html?id=control/basis/toolBar)、[鹰眼地图](http://mars2d.cn/editor-vue.html?id=control/basis/overviewMap)）。
- 瓦片图层：[WmsLayer](http://mars2d.cn/api/WmsLayer.html)、[WmtsLayer](http://mars2d.cn/api/WmtsLayer.html) 的弹窗在无要素时不再抛错；WMS 1.3.0 使用 crs 且 EPSG:4326 的 bbox 纬度在前；ArcGIS 紧凑切片释放 Blob URL；修复代理参数重复拼接；[ImageLayer](http://mars2d.cn/api/ImageLayer.html)、[ImageRotatedLayer](http://mars2d.cn/api/ImageRotatedLayer.html) 用 L.GeoJSON 替代已移除的 L.json；[SmTileLayer](http://mars2d.cn/api/SmTileLayer.html) 的 setUrl() 清空瓦片 URL 缓存，更换服务地址后不再请求旧地址。
- 图层：[ClusterLayer](http://mars2d.cn/api/ClusterLayer.html) 支持未上图先加数据，未上图时 show=false 不再抛错；[CanvasMarkerLayer](http://mars2d.cn/api/CanvasMarkerLayer.html) 支持未上图先加数据；[VirtualGrid](http://mars2d.cn/api/VirtualGrid.html) 平移不再累积 _cells，未上图时 remove、destroy 为安全空操作；[GeoJsonLayer](http://mars2d.cn/api/GeoJsonLayer.html)、[GraphicLayer](http://mars2d.cn/api/GraphicLayer.html)、[GroupLayer](http://mars2d.cn/api/GroupLayer.html) 在 show:false 时不渲染；[BusineDataLayer](http://mars2d.cn/api/BusineDataLayer.html) 的 onRemove 透传 map，修复 removeLayer、destroy 抛错。
- WFS：[WfsLayer](http://mars2d.cn/api/WfsLayer.html) 遇到 OWS 异常报文时回调 endfun，调用方不再永久等待；L.Filter.and/or/function 工厂不再把首个参数当作 thisArg，修复参数错位（示例：[OGC WFS服务](http://mars2d.cn/editor-vue.html?id=layer-graphic/wfs/ogc-wfs)）。
- 查询：天地图 POI（原 TdtPOI，现由 [QueryPOI](http://mars2d.cn/api/QueryPOI.html) 提供）的逆地理编码改用 fetchJson 解析响应体，与其它服务保持一致（示例：[POI点查询](http://mars2d.cn/editor-vue.html?id=query/poi)）。
- Canvas 系列：[CanvasImage](http://mars2d.cn/api/CanvasImage.html) 未指定渲染器时默认使用 L.Canvas，修复默认 SVG 渲染器下 addTo 抛出 `_updateImageOverlay is not a function` 的问题；[CanvasMarkerLayer](http://mars2d.cn/api/CanvasMarkerLayer.html) 在图标异步加载完成或图层已移除后不再绘制，iconAnchor、iconSize 缺省时按 0 处理。
- 图形对象：[Marker](http://mars2d.cn/api/Marker.html) 拖动监听去重、coordinates 赋值修正（Point、Circle、Ellipse 同步更新）；[Polyline](http://mars2d.cn/api/Polyline.html) 只设 text 不再崩溃，Canvas 渲染器下不再访问 _path；[MovingMarker](http://mars2d.cn/api/MovingMarker.html) 零时长段不再死循环；[PolyDecorator](http://mars2d.cn/api/PolyDecorator.html) 更新 bounds。
- 工具方法：[Util.getTemplateHtml](http://mars2d.cn/api/Util.html#.getTemplateHtml) 的字符串 format 不再吞掉整个模板；[Util.fetchBlob](http://mars2d.cn/api/Util.html#.fetchBlob) 失败时会 reject；属性值为 0、false 时不再被丢弃；[MarsArray](http://mars2d.cn/api/MarsArray.html) 支持 id=0，remove 不会误删末尾元素。
- 其它：[ArcGisImageLayer](http://mars2d.cn/api/ArcGisImageLayer.html) 多实例 id 不再共用；[MapVLayer](http://mars2d.cn/api/MapVLayer.html) 未传 data 时不再渲染失败；[EchartsLayer](http://mars2d.cn/api/EchartsLayer.html) 未初始化时事件回退到 Leaflet；[ExpImg](http://mars2d.cn/api/ExpImg.html) 未引入 domtoimage 时给出提示。
- [PointTrans.dms2degree](http://mars2d.cn/api/PointTrans.html#.dms2degree)：负值（南纬、西经）不再丢失符号，与 [degree2dms](http://mars2d.cn/api/PointTrans.html#.degree2dms) 互为逆运算（示例：[坐标拾取和转换](http://mars2d.cn/editor-vue.html?id=map/manager/pointTrans)）。
- 移除内部实现类 GaodePOI、GaodeRoute 残留的类级文档注释，二者不再出现在公开 API 文档中（对外统一使用 [QueryPOI](http://mars2d.cn/api/QueryPOI.html)、[QueryRoute](http://mars2d.cn/api/QueryRoute.html)）。

## 3.4.3 - 2026-09-10
#### 优化 💪
- [TileLayer](http://mars2d.cn/api/TileLayer.html)（XYZ 瓦片图层）为 EPSG:4326 坐标系时，支持叠加显示在 EPSG:3857 坐标系的地图中（示例：[4326底图](http://mars2d.cn/editor-vue.html?id=layer-tile/crs/epsg4326)）。
- [Ellipse](http://mars2d.cn/api/Ellipse.html) 增加绘制功能，对应 [DrawEllipse](http://mars2d.cn/api/DrawEllipse.html) 绘制类（示例：[Ellipse 椭圆](http://mars2d.cn/editor-vue.html?id=graphic/basis/ellipse)）。
- 优化 [PointTrans.degree2dms](http://mars2d.cn/api/PointTrans.html#.degree2dms) 方法（示例：[坐标拾取和转换](http://mars2d.cn/editor-vue.html?id=map/manager/pointTrans)）。
- [ToolButton](http://mars2d.cn/api/ToolButton.html) 支持设置 title 与 icon 图标（[setTitle](http://mars2d.cn/api/ToolButton.html#setTitle)、[setIcon](http://mars2d.cn/api/ToolButton.html#setIcon)）（示例：[自定义工具栏按钮](http://mars2d.cn/editor-vue.html?id=control/basis/toolButton)）。

## 3.4.2 - 2026-06-03
#### 修复 🔧
- [Map](http://mars2d.cn/api/Map.html) 的 [smallTooltip](http://mars2d.cn/api/Map.html#smallTooltip) 提示窗（[SmallTooltip](http://mars2d.cn/api/SmallTooltip.html)）无法通过 [enabled](http://mars2d.cn/api/SmallTooltip.html#enabled) 禁用（示例：[SmallTooltip 鼠标小提示窗](http://mars2d.cn/editor-vue.html?id=control/inside/smallTooltip)）。
- [Marker](http://mars2d.cn/api/Marker.html) 的 verticalOrigin 属性在旋转时的问题（示例：[Marker 图标点](http://mars2d.cn/editor-vue.html?id=graphic/basis/marker)）。

## 3.4.0 - 2026-02-14
#### 修复 🔧
- 通过右键菜单复制 [AntPath](http://mars2d.cn/api/AntPath.html) 时出错（示例：[动画效果线](http://mars2d.cn/editor-vue.html?id=graphic/basis/antpath)）。
- 修复其它已知问题。

## 3.3.7 - 2025-12-30
#### 优化 💪
- 插件产物中增加编译时间信息，便于排查问题。

#### 修复 🔧
- [GeoJsonLayer](http://mars2d.cn/api/GeoJsonLayer.html) 开启 mask 时 [flyTo](http://mars2d.cn/api/GeoJsonLayer.html#flyTo) 定位范围不准确（示例：[绘制反选遮罩层](http://mars2d.cn/editor-vue.html?id=layer-tile/manage/mask)）。
- [ClusterLayer](http://mars2d.cn/api/ClusterLayer.html) 单击 graphic 会触发 2 次事件（示例：[聚合点图层](http://mars2d.cn/editor-vue.html?id=layer-graphic/basis/cluster)）。

## 3.3.5 - 2025-10-25
#### 优化 💪
- 新增 [EmptyTileLayer](http://mars2d.cn/api/EmptyTileLayer.html) 空图层，便于切换到无底图（示例：[图层管理](http://mars2d.cn/editor-vue.html?id=layer-tile/manage/layers)）。
- [WmtsLayer](http://mars2d.cn/api/WmtsLayer.html) 增加 pickFeaturesUrl、popup、highlight 参数（示例：[OGC WMTS服务](http://mars2d.cn/editor-vue.html?id=layer-tile/type/wmts)）。
- [ArcGisLayer](http://mars2d.cn/api/ArcGisLayer.html) 增加 token 参数（示例：[ArcGIS MapServer](http://mars2d.cn/editor-vue.html?id=layer-tile/type/arcgis-tile)）。

## 3.3.4 - 2025-09-21
#### 优化 💪
- 矢量对象增加 setOptions 方法。
- [GraphicLayer](http://mars2d.cn/api/GraphicLayer.html) 增加 [loadJSON](http://mars2d.cn/api/GraphicLayer.html#loadJSON) 方法（示例：[graphic 矢量数据图层](http://mars2d.cn/editor-vue.html?id=layer-graphic/basis/graphicLayer)）。

#### 修复 🔧
- 编辑矢量对象时，编辑点的右键菜单无法正确获取（示例：[右键菜单](http://mars2d.cn/editor-vue.html?id=control/inside/contextmenu)）。
- [QueryPOI.getAddress](http://mars2d.cn/api/QueryPOI.html#getAddress) 调用后没有返回值（示例：[POI点查询](http://mars2d.cn/editor-vue.html?id=query/poi)）。
- 编辑矢量对象时，部分情况下未触发 editStop 事件（示例：[标绘](http://mars2d.cn/editor-vue.html?id=layer-graphic/draw/draw)）。
- 天地图 POI 服务的 offset 参数改为 count（示例：[POI点查询](http://mars2d.cn/editor-vue.html?id=query/poi)）。

## 3.3.3 - 2025-08-03
#### 新增 ⚡
- 新增 [Rain](http://mars2d.cn/api/Rain.html)、[Snow](http://mars2d.cn/api/Snow.html)、[BouncingMarker](http://mars2d.cn/api/BouncingMarker.html)、[PolyDecorator](http://mars2d.cn/api/PolyDecorator.html) 矢量对象（示例：[雨](http://mars2d.cn/editor-vue.html?id=graphic/basis/rain)、[雪](http://mars2d.cn/editor-vue.html?id=graphic/basis/snow)、[弹跳图标点](http://mars2d.cn/editor-vue.html?id=graphic/basis/bouncingMarker)、[线面装饰点](http://mars2d.cn/editor-vue.html?id=graphic/basis/polyDecorator)）。
- 矢量对象支持复制粘贴。

#### 优化 💪
- [Circle](http://mars2d.cn/api/Circle.html) 增加 diffuse 样式参数（示例：[Circle 圆](http://mars2d.cn/editor-vue.html?id=graphic/basis/circle)）。
- [Map](http://mars2d.cn/api/Map.html) 增加 [getLayrsTree](http://mars2d.cn/api/Map.html#getLayrsTree) 方法（示例：[图层管理](http://mars2d.cn/editor-vue.html?id=layer-tile/manage/layers)）。
- 新增 [PolyUtil.movePoints](http://mars2d.cn/api/PolyUtil.html#.movePoints) 方法。
- 新增功能示例：[旋转地图](http://mars2d.cn/editor-vue.html?id=map/manager/rotate)、[迁徙效果](http://mars2d.cn/editor-vue.html?id=graphic/basis/polyline-migration)、[有线上文本的折线](http://mars2d.cn/editor-vue.html?id=graphic/basis/polyline-text)、[时序轨迹路线](http://mars2d.cn/editor-vue.html?id=layer-graphic/other/trackplayback)。

#### 修复 🔧
- [WmsLayer](http://mars2d.cn/api/WmsLayer.html) 请求参数中去掉冗余的 url（示例：[OGC WMS服务](http://mars2d.cn/editor-vue.html?id=layer-tile/type/wms)）。
- [FineArrowYW](http://mars2d.cn/api/FineArrowYW.html) 最大点位修正为 2 个坐标（示例：[军事标绘](http://mars2d.cn/editor-vue.html?id=layer-graphic/draw/military)）。
- [AntPath](http://mars2d.cn/api/AntPath.html) 导出 JSON 出错（示例：[动画效果线](http://mars2d.cn/editor-vue.html?id=graphic/basis/antpath)）。
- [ArcGisFeatureLayer](http://mars2d.cn/api/ArcGisFeatureLayer.html) 点图标不显示（示例：[ArcGIS FeatureServer服务](http://mars2d.cn/editor-vue.html?id=layer-graphic/wfs/arcgis-feature)）。

## 3.3.2 - 2025-04-20
#### 新增 ⚡
- 新增 [BusineDataLayer](http://mars2d.cn/api/BusineDataLayer.html) 业务数据图层（示例：[业务后端数据图层](http://mars2d.cn/editor-vue.html?id=layer-graphic/basis/busineData)）。
- 新增 [KeyboardRoam](http://mars2d.cn/api/KeyboardRoam.html) 键盘漫游控制类（示例：[键盘漫游](http://mars2d.cn/editor-vue.html?id=map/manager/keyboardRoam)）。
- 新增 [QueryPOI](http://mars2d.cn/api/QueryPOI.html)、[QueryRoute](http://mars2d.cn/api/QueryRoute.html) 查询类，通过 service 参数选择天地图、百度或高德服务（示例：[POI点查询](http://mars2d.cn/editor-vue.html?id=query/poi)、[路径规划查询](http://mars2d.cn/editor-vue.html?id=query/route)）。

#### 优化 💪
- 线、面编辑时增加整体平移的编辑点（示例：[标绘](http://mars2d.cn/editor-vue.html?id=layer-graphic/draw/draw)）。
- [ClusterLayer](http://mars2d.cn/api/ClusterLayer.html) 增加 [clusterEnabled](http://mars2d.cn/api/ClusterLayer.html#clusterEnabled) 属性，可控制聚合开关（示例：[聚合点图层](http://mars2d.cn/editor-vue.html?id=layer-graphic/basis/cluster)）。
- [QueryGeoServer](http://mars2d.cn/api/QueryGeoServer.html) 增加点选查询（示例：[GeoServer矢量服务查询](http://mars2d.cn/editor-vue.html?id=query/geoserver)）。

#### 弃用 & API重构 🔒
- 移除 TdtPOI、BaiduPOI、GaodePOI、GaodeRoute 类，改用 [QueryPOI](http://mars2d.cn/api/QueryPOI.html)、[QueryRoute](http://mars2d.cn/api/QueryRoute.html)（示例：[POI点查询](http://mars2d.cn/editor-vue.html?id=query/poi)）。

## 3.3.1 - 2025-02-06
#### 新增 ⚡
- 新增 [AntPath](http://mars2d.cn/api/AntPath.html) 矢量对象（示例：[动画效果线](http://mars2d.cn/editor-vue.html?id=graphic/basis/antpath)）。

#### 优化 💪
- 线、面对象增加 dashSpeed 参数，可让虚线动起来（示例：[Polyline 线](http://mars2d.cn/editor-vue.html?id=graphic/basis/polyline)）。

## 3.3.0 - 2025-01-23
#### 新增 ⚡
- 线、面矢量对象增加 dashOffset 参数，用于控制虚线偏移（示例：[Polyline 线](http://mars2d.cn/editor-vue.html?id=graphic/basis/polyline)）。

#### 优化 💪
- [Rectangle](http://mars2d.cn/api/Rectangle.html)、[Circle](http://mars2d.cn/api/Circle.html) 的 [toGeoJSON](http://mars2d.cn/api/Circle.html#toGeoJSON) 增加 outline 参数（示例：[Rectangle 矩形](http://mars2d.cn/editor-vue.html?id=graphic/basis/rectangle)、[Circle 圆](http://mars2d.cn/editor-vue.html?id=graphic/basis/circle)）。
- 将 [AntPath](http://mars2d.cn/api/AntPath.html) 矢量对象纳入 SDK 统一管理（示例：[动画效果线](http://mars2d.cn/editor-vue.html?id=graphic/basis/antpath)）。

---

## 3.2.10 - 2024-12-22
#### 修复 🔧
- [LocationBar](http://mars2d.cn/api/LocationBar.html) 兼容平移全球地图时经度超过 180° 的情况（示例：[下侧状态栏](http://mars2d.cn/editor-vue.html?id=control/basis/locationBar)）。
- 修改矢量对象坐标时，部分对象的 label 坐标未同步更新。

#### 弃用 & API重构 🔒
- npm 包去掉 dist 子目录，与静态下载包的目录结构保持一致。若 `import "mars2d/dist/mars2d.css"` 报错，改为 `import "mars2d/mars2d.css"`。

## 3.2.6 - 2024-07-05
#### 优化 💪
- 矢量数据标绘时支持右键删除最后一个点位（示例：[标绘](http://mars2d.cn/editor-vue.html?id=layer-graphic/draw/draw)）。
- 控件增加 show 属性（示例：[控件的控制](http://mars2d.cn/editor-vue.html?id=control/basis/display)）。
- GeoJSON 数据加载支持 filter 参数筛选数据（示例：[GeoJson数据](http://mars2d.cn/editor-vue.html?id=layer-graphic/file/geojson)）。

#### 修复 🔧
- [ArcGisFeatureLayer](http://mars2d.cn/api/ArcGisFeatureLayer.html) 的 symbol 配置无效（示例：[ArcGIS FeatureServer服务](http://mars2d.cn/editor-vue.html?id=layer-graphic/wfs/arcgis-feature)）。
- 优化 [Marker](http://mars2d.cn/api/Marker.html) 的 label 样式参数（示例：[图标点+文字](http://mars2d.cn/editor-vue.html?id=graphic/basis/marker-labe)）。
- [Polyline](http://mars2d.cn/api/Polyline.html) 多色线缩放时颜色异常变化（示例：[Polyline 线](http://mars2d.cn/editor-vue.html?id=graphic/basis/polyline)）。
- 矢量对象附带的文本在部分情况下未跟随坐标变动（示例：[有线上文本的折线](http://mars2d.cn/editor-vue.html?id=graphic/basis/polyline-text)）。

## 3.2.4 - 2024-04-21
#### 优化 💪
- 优化 [ToolBar](http://mars2d.cn/api/ToolBar.html) 样式（示例：[工具按钮栏](http://mars2d.cn/editor-vue.html?id=control/basis/toolBar)）。
- [EchartsLayer](http://mars2d.cn/api/EchartsLayer.html) 增加 [on](http://mars2d.cn/api/EchartsLayer.html#on)、[off](http://mars2d.cn/api/EchartsLayer.html#off) 事件绑定（示例：[饼形图标记](http://mars2d.cn/editor-vue.html?id=layer-other/echarts/marker-pie)）。
- [Marker](http://mars2d.cn/api/Marker.html)、[Label](http://mars2d.cn/api/Label.html)、[DivGraphic](http://mars2d.cn/api/DivGraphic.html) 增加 minZoom、maxZoom 参数，限定显示层级（示例：[Marker 图标点](http://mars2d.cn/editor-vue.html?id=graphic/basis/marker)、[Label 文本](http://mars2d.cn/editor-vue.html?id=graphic/basis/label)、[DivGraphic DIV点](http://mars2d.cn/editor-vue.html?id=graphic/divGraphic/basis)）。

## 3.2.1 - 2024-02-22
#### 新增 ⚡
- 矢量对象增加 label 附加文本属性（示例：[图标点+文字](http://mars2d.cn/editor-vue.html?id=graphic/basis/marker-labe)）。

#### 优化 💪
- 新增 KML、SHP 格式文件的加载示例（[KML](http://mars2d.cn/editor-vue.html?id=layer-graphic/file/kml2json)、[SHP](http://mars2d.cn/editor-vue.html?id=layer-graphic/file/shp2json)）。
- 重写 [Util.template](http://mars2d.cn/api/Util.html#.template) 方法。

#### 修复 🔧
- [ClusterLayer](http://mars2d.cn/api/ClusterLayer.html) 聚合图层的 [bindPopup](http://mars2d.cn/api/ClusterLayer.html#bindPopup) 无效（示例：[聚合点图层](http://mars2d.cn/editor-vue.html?id=layer-graphic/basis/cluster)）。

## 3.2.0 - 2024-01-16
#### 新增 ⚡
- 矢量对象增加 show 属性。
- 矢量对象增加 hasEdit、isAutoEditing 参数（示例：[标绘](http://mars2d.cn/editor-vue.html?id=layer-graphic/draw/draw)）。

---

## 3.1.25 - 2023-12-31
#### 修复 🔧
- [Polygon.toJSON](http://mars2d.cn/api/Polygon.html#toJSON) 导出异常（示例：[Polygon 面](http://mars2d.cn/editor-vue.html?id=graphic/basis/polygon)）。
- 瓦片图层传入 show:false 无效（示例：[图层管理](http://mars2d.cn/editor-vue.html?id=layer-tile/manage/layers)）。

## 3.1.22 - 2023-10-27
#### 修复 🔧
- EPSG:4490 坐标系下天地图显示异常（示例：[天地图](http://mars2d.cn/editor-vue.html?id=layer-tile/online/tdt)）。
- [ExpImg](http://mars2d.cn/api/ExpImg.html) 导出图片未传入回调（示例：[场景出图](http://mars2d.cn/editor-vue.html?id=thing/expImg)）。
- 部分情况下更新 style 后，fill、outline 被自动显示（示例：[style样式](http://mars2d.cn/editor-vue.html?id=graphic/base/style)）。

## 3.1.20 - 2023-09-13
#### 新增 ⚡
- 新增 TdtPOI 查询类，v3.3.2 起由 [QueryPOI](http://mars2d.cn/api/QueryPOI.html) 统一提供（示例：[POI点查询](http://mars2d.cn/editor-vue.html?id=query/poi)）。

#### 优化 💪
- 矢量对象支持 zIndex 属性。
- 优化 [Circle](http://mars2d.cn/api/Circle.html) 圆的绘制规则（示例：[Circle 圆](http://mars2d.cn/editor-vue.html?id=graphic/basis/circle)）。

#### 弃用 & API重构 🔒
- 弃用 mars2d-widget 插件，原生 JS 技术栈的项目直接改用源码 es5-widget.js。

## 3.1.17 - 2023-07-03
#### 修复 🔧
- graphic、[GraphicLayer](http://mars2d.cn/api/GraphicLayer.html) 的 pane 参数无效（示例：[graphic 矢量数据图层](http://mars2d.cn/editor-vue.html?id=layer-graphic/basis/graphicLayer)）。
- 修复 v3.1.15 引入的 [OverviewMap](http://mars2d.cn/api/OverviewMap.html) 出现 2 个矩形框的问题（示例：[鹰眼地图](http://mars2d.cn/editor-vue.html?id=control/basis/overviewMap)）。
- [Map](http://mars2d.cn/api/Map.html) 的 addLayer、removeLayer 事件无效（示例：[map相关事件](http://mars2d.cn/editor-vue.html?id=map/control/event)）。

## 3.1.16 - 2023-06-05
#### 新增 ⚡
- 聚合图层支持右键菜单（示例：[右键菜单](http://mars2d.cn/editor-vue.html?id=control/inside/contextmenu)）。

#### 修复 🔧
- 线、面编辑时，外部修改坐标后，图上的编辑点未同步移动（示例：[标绘](http://mars2d.cn/editor-vue.html?id=layer-graphic/draw/draw)）。
- 修复 v3.1.15 引入的 [ExpImg](http://mars2d.cn/api/ExpImg.html) 导出图片出错（示例：[场景出图](http://mars2d.cn/editor-vue.html?id=thing/expImg)）。
- [PointTrans.latlng2coord](http://mars2d.cn/api/PointTrans.html#.latlng2coord) 在没有高度时不再返回 0（示例：[坐标拾取和转换](http://mars2d.cn/editor-vue.html?id=map/manager/pointTrans)）。

## 3.1.15 - 2023-05-23
#### 重要说明 📣
- Leaflet 升级至 [1.9.4](https://github.com/Leaflet/Leaflet/releases/tag/v1.9.4)。

#### 新增 ⚡
- [GraphicLayer](http://mars2d.cn/api/GraphicLayer.html) 增加 [bringToBack](http://mars2d.cn/api/GraphicLayer.html#bringToBack)、[bringToFront](http://mars2d.cn/api/GraphicLayer.html#bringToFront) 方法（示例：[graphic 矢量数据图层](http://mars2d.cn/editor-vue.html?id=layer-graphic/basis/graphicLayer)）。
- [Map](http://mars2d.cn/api/Map.html) 增加 [isLoading](http://mars2d.cn/api/Map.html#isLoading) 属性和地图加载完成时的 load 事件（示例：[map相关事件](http://mars2d.cn/editor-vue.html?id=map/control/event)）。

#### 修复 🔧
- [GroupLayer](http://mars2d.cn/api/GroupLayer.html) 的 zIndex 设置无效（示例：[图层管理](http://mars2d.cn/editor-vue.html?id=layer-tile/manage/layers)）。
- 修复谷歌在线地图服务（示例：[谷歌](http://mars2d.cn/editor-vue.html?id=layer-tile/online/google)）。
- [ExpImg.expByDraw](http://mars2d.cn/api/ExpImg.html#expByDraw) 按区域截图后未恢复地图状态（示例：[场景出图](http://mars2d.cn/editor-vue.html?id=thing/expImg)）。

## 3.1.14 - 2023-04-24
#### 新增 ⚡
- 大部分图层支持透明度（opacity）设置（示例：[图层管理](http://mars2d.cn/editor-vue.html?id=layer-tile/manage/layers)）。

#### 修复 🔧
- [Marker](http://mars2d.cn/api/Marker.html) 部分图标定位偏移（示例：[Marker 图标点](http://mars2d.cn/editor-vue.html?id=graphic/basis/marker)）。

## 3.1.12 - 2023-03-20
#### 新增 ⚡
- 新增 [SmTileLayer](http://mars2d.cn/api/SmTileLayer.html) 超图瓦片服务图层（示例：[超图瓦片](http://mars2d.cn/editor-vue.html?id=layer-tile/type/sm-tile)）。

## 3.1.10 - 2023-01-10
#### 重要说明 📣
- Leaflet 升级至 [1.9.3](https://github.com/Leaflet/Leaflet/releases/tag/v1.9.3)。

#### 修复 🔧
- 修正 mars2d.d.ts 中的错误。
- 修复全屏按钮多次切换的问题（示例：[工具按钮栏](http://mars2d.cn/editor-vue.html?id=control/basis/toolBar)）。

## 3.1.9 - 2022-11-30
#### 优化 💪
- 量算类增加绘制、编辑事件的抛出（示例：[量算](http://mars2d.cn/editor-vue.html?id=thing/measure)）。
- 新增 rightClick 右键事件（示例：[map相关事件](http://mars2d.cn/editor-vue.html?id=map/control/event)）。
- 矢量数据增加销毁方法。

#### 修复 🔧
- 地图与矢量数据的右键菜单绑定后出现叠加（示例：[右键菜单](http://mars2d.cn/editor-vue.html?id=control/inside/contextmenu)）。
- snake 路线多次停止、开启后运行异常（示例：[线的运动动画](http://mars2d.cn/editor-vue.html?id=graphic/basis/polyline-snakeIn)）。
- 地图 scale（比例尺）控件的参数无法配置（示例：[比例尺](http://mars2d.cn/editor-vue.html?id=control/leaflet/scale)）。
- [MapSplit](http://mars2d.cn/api/MapSplit.html) 控件支持数组形式的图层配置（示例：[卷帘对比](http://mars2d.cn/editor-vue.html?id=control/basis/mapSplit)）。

## 3.1.7 - 2022-10-24
#### 重要说明 📣
- Leaflet 升级至 [1.9.2](https://github.com/Leaflet/Leaflet/releases/tag/v1.9.2)。

#### 优化 💪
- [WfsLayer](http://mars2d.cn/api/WfsLayer.html)、[ArcGisFeatureLayer](http://mars2d.cn/api/ArcGisFeatureLayer.html) 等图层增加 [flyTo](http://mars2d.cn/api/WfsLayer.html#flyTo) 方法（示例：[OGC WFS服务](http://mars2d.cn/editor-vue.html?id=layer-graphic/wfs/ogc-wfs)）。

#### 修复 🔧
- snakeIn 路线 style 中的颜色传值无效（示例：[线的运动动画](http://mars2d.cn/editor-vue.html?id=graphic/basis/polyline-snakeIn)）。
- [Circle](http://mars2d.cn/api/Circle.html) 绘制过程中 radius 未动态回传（示例：[标绘](http://mars2d.cn/editor-vue.html?id=layer-graphic/draw/draw)）。
- [Util.formatDate](http://mars2d.cn/api/Util.html#.formatDate) 格式化无效。

## 3.1.6 - 2022-09-16
#### 优化 💪
- 重构 Vue 示例与项目 UI。

#### 新增 ⚡
- 矢量数据增加 toJSON 方法。

## 3.1.5 - 2022-08-01
#### 优化 💪
- 优化 [Map](http://mars2d.cn/api/Map.html) 内部图层的存储与读取方式（示例：[图层管理](http://mars2d.cn/editor-vue.html?id=layer-tile/manage/layers)）。

#### 弃用 & API重构 🔒
- 图层、矢量数据类弃用 uuid 属性，统一改用 [id](http://mars2d.cn/api/GraphicLayer.html#id)。

## 3.1.4 - 2022-06-26
#### 新增 ⚡
- [GeoJsonLayer](http://mars2d.cn/api/GeoJsonLayer.html) 增加 chinaCRS 参数，支持数据自动纠偏（示例：[底图纠偏](http://mars2d.cn/editor-vue.html?id=layer-tile/manage/chinaCRS)）。

#### 优化 💪
- 重写 Vue 功能示例编辑器。
- 主库和插件库中第三方依赖 JS 库未引入时给出错误提示，便于排查问题。

#### 修复 🔧
- [GraphicLayer.openPopup](http://mars2d.cn/api/GraphicLayer.html#openPopup) 偶发报错（示例：[Popup鼠标单击信息窗](http://mars2d.cn/editor-vue.html?id=control/inside/popup)）。
- [GeoJsonLayer](http://mars2d.cn/api/GeoJsonLayer.html) 的 popupOptions 参数未生效（示例：[GeoJson数据](http://mars2d.cn/editor-vue.html?id=layer-graphic/file/geojson)）。

## 3.1.3 - 2022-04-29
#### 重要说明 📣
- Leaflet 升级至 [1.8.0](https://github.com/Leaflet/Leaflet/releases/tag/v1.8.0)。
- 发布 v3.1 版本。
- SDK 内部重新架构。

#### 新增 ⚡
- 新增 [MapSplit](http://mars2d.cn/api/MapSplit.html) 双屏对比控件（示例：[双屏对比](http://mars2d.cn/editor-vue.html?id=map/double/compare)）。
- 更新 [mars2d.Token](http://mars2d.cn/api/Token.html) 的所有默认值。
- 新增 [Token.updateAll](http://mars2d.cn/api/Token.html#.updateAll) 方法，便于外部批量更新。

#### 修复 🔧
- 修正部分 [DivGraphic](http://mars2d.cn/api/DivGraphic.html) 拖拽后的定位偏差（示例：[DivGraphic DIV点](http://mars2d.cn/editor-vue.html?id=graphic/divGraphic/basis)）。
- 修复其它已知问题。

## 3.0.9 - 2022-03-08
#### 新增 ⚡
- [Circle](http://mars2d.cn/api/Circle.html) 增加 [outlineLatlngs](http://mars2d.cn/api/Circle.html#outlineLatlngs) 属性（示例：[Circle 圆](http://mars2d.cn/editor-vue.html?id=graphic/basis/circle)）。
- 新增 [QueryArcServer](http://mars2d.cn/api/QueryArcServer.html)、[QueryGeoServer](http://mars2d.cn/api/QueryGeoServer.html) 查询类（示例：[ArcGIS Server矢量服务查询](http://mars2d.cn/editor-vue.html?id=query/arcgis)、[GeoServer矢量服务查询](http://mars2d.cn/editor-vue.html?id=query/geoserver)）。
- 新增一批功能示例。

#### 修复 🔧
- 自由线（brush）绘制偶发报错（示例：[标绘](http://mars2d.cn/editor-vue.html?id=layer-graphic/draw/draw)）。
- 量算结果编辑时出现异常（示例：[量算](http://mars2d.cn/editor-vue.html?id=thing/measure)）。
- 高德 POI 查询（原 GaodePOI，现由 [QueryPOI](http://mars2d.cn/api/QueryPOI.html) 提供）中限定区域无效（示例：[POI点查询](http://mars2d.cn/editor-vue.html?id=query/poi)）。

## 3.0.8 - 2022-02-25
#### 重要说明 📣
- Vue 版基础项目上线发布。
- 原生 JS 版功能示例优化，与 Vue 版保持一致。

#### 新增 ⚡
- 新增 [ToolButton](http://mars2d.cn/api/ToolButton.html) 控件（示例：[自定义工具栏按钮](http://mars2d.cn/editor-vue.html?id=control/basis/toolButton)）。
- 完善 API 文档与 TypeScript 定义。

## 3.0.7 - 2022-02-20
#### 重要说明 📣
- Vue 版功能示例上线发布。

#### 新增 ⚡
- [WmsLayer](http://mars2d.cn/api/WmsLayer.html) 增加 click 事件与 popup 支持（示例：[OGC WMS服务](http://mars2d.cn/editor-vue.html?id=layer-tile/type/wms)）。
- 新增 [ToolButton](http://mars2d.cn/api/ToolButton.html) 控件（示例：[自定义工具栏按钮](http://mars2d.cn/editor-vue.html?id=control/basis/toolButton)）。
- 新增 mars2d.d.ts，提供 TypeScript 类型支持。

#### 修复 🔧
- 核对并修正 API 文档中的描述错误。
- 修复 v3.0.5 修改 show 后瓦片图层不显示的问题（示例：[图层管理](http://mars2d.cn/editor-vue.html?id=layer-tile/manage/layers)）。
- 圆、矩形绘制完成后激活编辑失败（示例：[Circle 圆](http://mars2d.cn/editor-vue.html?id=graphic/basis/circle)、[Rectangle 矩形](http://mars2d.cn/editor-vue.html?id=graphic/basis/rectangle)）。
- 完成一轮测试，修复一批问题。

#### 弃用 & API重构 🔒
- 移除 axios 库，改用 [Util.fetchJson](http://mars2d.cn/api/Util.html#.fetchJson) 或 [Util.sendAjax](http://mars2d.cn/api/Util.html#.sendAjax)。
- 优化 PBF 图层：[PbfLayer](http://mars2d.cn/api/PbfLayer.html) 的 vectorTileLayerStyles 参数改名为 style，并简化参数形式（示例：[pbf矢量瓦片服务](http://mars2d.cn/editor-vue.html?id=layer-graphic/wfs/pbf)）。

## 3.0.5 - 2022-01-17
#### 优化 💪
- 图层增加 show 参数与属性（示例：[图层管理](http://mars2d.cn/editor-vue.html?id=layer-tile/manage/layers)）。
- 优化状态栏在小分辨率下的显示（示例：[下侧状态栏](http://mars2d.cn/editor-vue.html?id=control/basis/locationBar)）。

#### 修复 🔧
- 修复已知问题。

## 3.0.3 - 2021-12-17
#### 重要说明 📣
- Leaflet 升级至 [1.7.1](https://github.com/Leaflet/Leaflet/releases/tag/v1.7.1)。
- 完成 V2 全部功能示例的 V3 新版开发。
- v3.0 正式稳定版发布。
- 优化 SDK 内部接口方法，整理并发布 API 文档。
- 完成教程编写。

#### 修复 🔧
- 完成一轮测试并修复已知缺陷。

## 3.0.0 - 2021-11-16
#### 重要说明 📣
- 发布 v3.0 版本。
- **易学**：用法与语法按开发者使用习惯设计，降低上手门槛，初级开发者即可使用。
- **规范**：API 从顶层统一规划、从零重构，插件收敛进 SDK，对外提供统一规范的 API。
- **高效**：提升开发效率与平台渲染效率。
- **文档完善**：重写教程文档，基于 SDK 注释自动生成详尽的 API 文档，完全免费开放。
- **配套示例**：提供 Vue 版功能示例与基础项目模板。
- **免费**：免费、无限制使用。

#### 新增 ⚡
- 矢量数据：全新设计矢量数据体系，以 Graphic 矢量对象（统一的规范与 style 设计）配合 [GraphicLayer](http://mars2d.cn/api/GraphicLayer.html) 矢量图层统一管理（示例：[Marker 图标点](http://mars2d.cn/editor-vue.html?id=graphic/basis/marker)）。
- GeoJSON 图层：新增 [GeoJsonLayer](http://mars2d.cn/api/GeoJsonLayer.html)，可在 symbol 中通过 type 参数指定 Graphic 类型来渲染（示例：[GeoJson数据](http://mars2d.cn/editor-vue.html?id=layer-graphic/file/geojson)）。

#### 弃用 & API重构 🔒
- v3.0 与 v2.x 不兼容（API 结构不同），无法平滑升级：v3 的全部代码均为从零编写，并非基于旧版本修改。

---

## 2.0.0 - 2020-01-01
#### 重要说明 📣
- 发布 v2.0。

## 1.0.0 - 2017-08-25
#### 重要说明 📣
- 发布 v1.0。
