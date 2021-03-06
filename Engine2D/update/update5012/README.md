
## 概述

白鹭引擎包含了白鹭时代研发的遵循HTML5标准的游戏引擎。他包括 2D / 3D 渲染核心、GUI体系、音频管理、资源管理等游戏引擎的常用模块。

通过使用白鹭引擎，开发者可以尽可能的不用关注浏览器的底层实现，解决HTML5游戏性能问题及碎片化问题，灵活地满足开发者开发2D或3D游戏的需求。

## 更新内容

* 2D 渲染 - JavaScript
    * 修复 canvasScaleFactor 大于1时绘制异常问题 (感谢论坛开发者 zyy)
    * 修复 exml 加载异常出现脏数据问题 (感谢论坛开发者 xtcel5805)
    * 修复解析 exml 使用 eval 函数导致某些环境下内存过大问题

## 已知问题

* 开发者如果使用 WebAssembly 渲染，目前会在类的静态变量声明处创建对象时报错

## 修复 canvasScaleFactor 大于一时绘制异常问题
当 canvasScaleFactor 大于1的情况下，如果显示对象被设置滤镜或者不规则遮罩后，渲染位置可能会发生偏移。

## 修复 exml 加载异常出现脏数据问题
exml 加载异常后，会解析为一个 null 的数据并缓存，当下一次加载会直接返回这个为 null 的数据，这个行为是不正确的，这导致后续彻底无法正确加载这个皮肤了。

## 修复解析 exml 使用 eval 函数导致某些环境下内存过大问题
某些环境下，直接使用 eval 函数会产生内存问题，我们通过一些修改修复了这个问题。[参考文档](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/eval)
