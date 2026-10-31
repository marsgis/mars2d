# Mars2D 二维地图客户端开发平台

<p align="center">
<img src="http://mars2d.cn/logo.png" width="300px" />
</p>

<p align="center">🌎 一款免费的二维地图客户端开发平台</p>

<p align="center">
<a target="_black" href="https://github.com/marsgis/mars2d">
<img alt="GitHub stars" src="https://img.shields.io/github/stars/marsgis/mars2d?style=flat&logo=github">
</a>
<a target="_black" href="https://www.npmjs.com/package/mars2d">
<img alt="Npm downloads" src="https://img.shields.io/npm/dt/mars2d?style=flat&logo=npm">
</a>
<a target="_black" href="https://www.npmjs.com/package/mars2d">
<img alt="Npm version" src="https://img.shields.io/npm/v/mars2d.svg?style=flat&logo=npm&label=version"/>
</a>
</p>

[**English**](./README_EN.md) | [**中文**](./README.md)

## 平台介绍

Mars2D 是一款免费的二维地图客户端开发平台，基于 [Leaflet](http://leafletjs.com/) 优化提升与 B/S 架构设计，支持多行业扩展的轻量级高效能 GIS 开发平台。提供大数据可视化、实时流数据可视化能力，可快速实现浏览器和移动端上美观、流畅的地图呈现与空间分析。

- 官网：[http://mars2d.cn](http://mars2d.cn)
- 开发教程：[http://mars2d.cn/docs/](http://mars2d.cn/docs/)
- API 文档：[http://mars2d.cn/api/](http://mars2d.cn/api/)
- 更新日志：[CHANGE.md](./CHANGE.md)
- 问题反馈：[Gitee Issues](https://gitee.com/marsgis/mars2d/issues)

Mars2D 所有资料和代码均免费开源；本仓库同时作为 Mars2D 开源仓库的导航页。



## 示例、模板与项目导航

### 功能示例

对平台每个功能编写的案例代码，可以阅读每个示例代码来学习各功能，与官网功能示例一致效果。

| 说明 | 教程 | 视频 | Github 源码 | 国内 Gitee 源码 |
|---|---|---|---|---|
| 原生 JS 版 | [查看](http://mars2d.cn/docs/guide/example-es5/) | 暂无 | [mars2d-es5-example](https://github.com/marsgis/mars2d-es5-example) | [mars2d-es5-example](https://gitee.com/marsgis/mars2d-es5-example) |
| Vue 版 | [查看](http://mars2d.cn/docs/guide/example-vue/) | [查看](https://www.bilibili.com/video/BV1pb4y1W7NG/) | [mars2d-vue-example](https://github.com/marsgis/mars2d-vue-example) | [mars2d-vue-example](https://gitee.com/marsgis/mars2d-vue-example) |




### 最简项目模板

提供原生 JS、Vue、React、Angular、Electron、uni-app 等技术栈的最简项目模板，已统一维护在一个仓库：

- Github：[mars2d-templates](https://github.com/marsgis/mars2d-templates)
- Gitee：[mars2d-templates](https://gitee.com/marsgis/mars2d-templates)

可直接使用或参考这些模板，快速了解 SDK 在不同技术栈项目中如何引入。

### 基础项目

基础项目具备一个 GIS 项目常见功能，只需更换数据及叠加业务即可完成项目交付。更多功能可考虑[付费项目模板](http://mars2d.cn/buy.html)。

| 说明 | 教程 | 视频 | Github 源码 | 国内 Gitee 源码 |
|---|---|---|---|---|
| 基础项目 Vue 版 | [查看](http://mars2d.cn/docs/guide/project-vue/) | [查看](https://www.bilibili.com/video/BV1DR4y1G75T/) | [mars2d-vue-project](https://github.com/marsgis/mars2d-vue-project) | [mars2d-vue-project](https://gitee.com/marsgis/mars2d-vue-project) |
| app项目 | [查看](http://mars2d.cn/docs/guide/project-app/) | 无 |  | |
| 基础项目 原生 JS 版 | [查看](http://mars2d.cn/docs/guide/project-es5/) | 无 | [mars2d-es5-project](https://github.com/marsgis/mars2d-es5-project) | [mars2d-es5-project](https://gitee.com/marsgis/mars2d-es5-project) |




### 在线效果

#### 功能示例

[在线体验](http://mars2d.cn/example.html)

![功能示例](http://marsgis.cn/img/project/mars2d-doc/example1.jpg)

#### 基础项目

[在线体验](http://mars2d.cn/project/vue/jcxm.html)

![基础项目](http://marsgis.cn/img/project/mars2d-vue-project-jcxm/1.jpg)

#### 综合态势项目

[在线体验](http://mars2d.cn/project/vue/index.html)

![综合态势项目](http://marsgis.cn/img/project/mars2d-vue-project-zhts/1.jpg)





## 授权协议

Mars2D SDK 采用 **“社区免费版 + 商业授权版”** 双重授权。

[![License](https://img.shields.io/badge/license-Apache--2.0%20%2B%20Mars2D%20Additional%20Terms-blue)](./LICENSE)

- **社区免费版**：基于 **Apache License 2.0**，并附加《Mars2D 免费版附加条款》。可免费用于学习、开发与商业项目，但**必须保留**软件运行时页面周边的 **Mars2D Logo** 和浏览器 **F12 控制台**输出的版权信息，**不得移除、遮挡、修改或通过任何技术手段规避**。
- **商业授权版**：付费后可**去除页面 Logo**，F12 控制台信息替换为贵单位/项目名称，并提供盖章授权文件、专属技术支持与缺陷修复服务；**不限制项目数、节点数、用户数和使用期限**，按 SDK 大版本授权。

| | 社区免费版 | 商业授权版 |
| --- | --- | --- |
| 页面 Logo | ✅ 必须保留 | ❌ 已移除 |
| F12 控制台信息 | 通用版权信息（须保留） | 显示贵单位名称 |
| 授权费用 | 免费 | 按大版本一次性付费 |
| 数量 / 期限限制 | 无 | 无 |
| 商业交付 / 招投标 | 须保留署名 | 提供盖章授权，合规无忧 |

📘 完整协议：[`LICENSE`](./LICENSE) ｜ [购买授权](http://mars2d.cn/buy.html)
