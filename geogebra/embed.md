---
title: "geogebra 图形嵌入网页，Hexo文章"
source: "https://www.zywvvd.com/notes/tools/geogebra/geogebra-html-embed/geogebra-html-embed/"
author:
  - "[[Yiwei Zhang]]"
published: 2020-12-19
created: 2025-06-02
description: "geogebra是优秀的数学绘图工具，可以描述数学图像并演示，支持互动，功能强大。本文介绍将geogebra嵌入网页的方法。"
tags:
  - "clippings"
---

本文最后更新于：2025年4月30日 下午

> geogebra是优秀的数学绘图工具，可以描述数学图像并演示，支持互动，功能强大。本文介绍将geogebra嵌入网页的方法。

### 需求描述

> `geogebra` 的强大功能勾引着我想要在自己的博客里实现演示功能，有一些自己设定的需求：

- 可以展示我自己设计的 `geogebra` 图形；
- 带有滑块可以互动控制；
- 可以支持动画自动演示；
- 不要带其他编辑控件，仅能控制我设计的部分；
- 可以控制显示的图形按钮；
- 不依赖 `geogebra` 官网，搭建属于自己的服务；
- 可以方便地在博客/网页中插入、编辑、删除各个演示内容；
- 不依赖已经分享好的链接，仅依赖实际演示图信息；
- 速度不能太慢；
- 演示图形要居中。

### 调研报告

> 为满足上述需求我做了几天的调研，网上清楚明白说这个事情的信息很少，而且很杂乱，我把我获取到的信息汇总在这里。

#### geogebra

- 官方网站： [https://www.geogebra.org/](https://www.zywvvd.com/pages/go.html?goUrl=https%3A%2F%2Fwww.geogebra.org%2F)
- 当前流行的版本主要是 `geogebra 5` 和 `geogebra 6`
- `geogebra 5` 更加经典，可以导出动画，6不支持动画导出
- 二者可以导出 `ggb文件` 和html代码
- 但是使用官方html代码得到的演示图必须带编辑工具控件，删除会使图形失效

#### desmos

- `desmos` 也是类似的数学画板工具，加载很快，嵌入链接分享很方便，使用逻辑和 `geogebra` 几乎相同
- 有一个不得不弃用的问题是导出的演示图不带滑块，无法动态互动

#### geogebra 图形信息

- 事实上绘制好的图形信息是有固定格式的
- 为了唯一确定该信息并在别处引用，我目前了解到四种方法：
	- `material_id` ： 一些在 `geogebra` 官网上的图形有固定的唯一ID，可以将其作为确定内容的标识
	- `ggb文件` ： 直接记录和保存图形信息的文件
	- `ggbBase64代码` ：将图形信息编码成字符串的一种信息保存方式，从信息量来看和 `ggb文件` 是等价的
	- 分享链接：可以将编辑好的图形上传到 `geogebra` 官网上，官网生成唯一的链接返回来用于分享
- 四种方式中，分享链接是最方便的，不需要对博客/网页项目进行任何修改，用 `iframe` 插入引用控件，直接引入来自官网的图形
- material\_id我还不知道如何获取，了解不多，而且因为这个ID不包含任何内容信息，总有一种不靠谱的感觉
- 我比较信赖的 `geogebra` 图形引用形式还是 `ggb文件` 和 `ggbBase64代码` 的引用方式
- 选中别人分享的图形，按下快捷键 `ctrl + shift + B` 可以复制该图形的 `ggbBase64` 代码

#### 学习资料

- `geogebra` 制作的教程千千万，在此不表，本文主要关注图形嵌入网页的教程
- 网页嵌入官方教程： [https://wiki.geogebra.org/en/Reference:GeoGebra\_App\_Parameters](https://www.zywvvd.com/pages/go.html?goUrl=https%3A%2F%2Fwiki.geogebra.org%2Fen%2FReference%3AGeoGebra_App_Parameters)

> 目前见到满足我需求最靠谱的站长，在此感谢大神分享，大家有需要也可以去他的站点学习

- [https://kz16.top/](https://www.zywvvd.com/pages/go.html?goUrl=https%3A%2F%2Fkz16.top%2F)

> 也是这位大佬，在B站发布的视频教程，很良心

- [https://www.bilibili.com/video/av80321187/](https://www.zywvvd.com/pages/go.html?goUrl=https%3A%2F%2Fwww.bilibili.com%2Fvideo%2Fav80321187%2F)

### 网页嵌入方法

#### iframe

> `iframe` 元素会创建包含另外一个文档的内联框架（即行内框架）。

##### 获取geogebra图形的iframe代码

- 打开 `geogebra 6` （网页版、客户端都可以）， [https://www.geogebra.org/classic](https://www.zywvvd.com/pages/go.html?goUrl=https%3A%2F%2Fwww.geogebra.org%2Fclassic) 并编辑内容
- 分享后获得分享链接，替换 `src` 内容部分
- 此处以 [https://blog.csdn.net/fatty\_zhu/article/details/77411254的示例src为例：](https://www.zywvvd.com/pages/go.html?goUrl=https%3A%2F%2Fblog.csdn.net%2Ffatty_zhu%2Farticle%2Fdetails%2F77411254%25E7%259A%2584%25E7%25A4%25BA%25E4%25BE%258Bsrc%25E4%25B8%25BA%25E4%25BE%258B%25EF%25BC%259A)
```
<iframe scrolling="no" title="布丰投针实验" src="https://www.geogebra.org/material/iframe/id/A25F9Tzs/width/1347/height/598/border/888888/smb/false/stb/false/stbh/false/ai/false/asb/false/sri/true/rc/false/ld/false/sdz/true/ctl/false" width="800px" height="400px"></iframe>
```
- 上述代码放在单独的html文件中即可运行

#### 官网js解析ggb文件信息

- 将画好的图形下载成 `ggb文件` 格式
- 将该文件上传到网络（不允许读取本地的文件），链接必须为 `http, data, chrome, chrome-extension, chrome-untrusted, https` 类型之一。
- 获取文件链接，以我的链接 [https://uipv4.zywvvd.com:33030/HexoFiles/images\_matrixtime/20201219164932.ggb](https://uipv4.zywvvd.com:33030/HexoFiles/images_matrixtime/20201219164932.ggb) 为例
- 向html文件黏贴代码：
```xml
<script src="https://cdn.geogebra.org/apps/deployggb.js"></script><div id="ggbApplet"></div><script>var parameters = {"id": "ggbApplet","width":468,"height":492,"showToolBar":true,"language":"zh","filename":"https://uipv4.zywvvd.com:33030/HexoFiles/images_matrixtime/20201219164932.ggb",};// is3D=is 3D applet using 3D view, AV=Algebra View, SV=Spreadsheet View, CV=CAS View, EV2=Graphics View 2, CP=Construction Protocol, PC=Probability Calculator DA=Data Analysis, FI=Function Inspector, macro=Macrosvar views = {'is3D': 0,'AV': 0,'SV': 0,'CV': 0,'EV2': 0,'CP': 0,'PC': 0,'DA': 0,'FI': 0,'macro': 0};var applet = new GGBApplet(parameters, '5.0', views);window.onload = function() {applet.inject('ggbApplet')};applet.setPreviewImage('data:image/gif;base64,R0lGODlhAQABAAAAADs=','https://www.geogebra.org/images/GeoGebra_loading.png','https://www.geogebra.org/images/applet_play.png');</script>
```

#### 官网js解析ggbBase64信息

- ##### 事实上就是按照官方教程行事 https://wiki.geogebra.org/en/Reference:GeoGebra\_App\_Parameters
- 获取 `ggbBase64` 可以在 [https://geogebra.kz16.top/](https://www.zywvvd.com/pages/go.html?goUrl=https%3A%2F%2Fgeogebra.kz16.top%2F) 上作图，直接得到代码
- 也可以将画好的图形下载成 `网页.html` 格式

[![](https://uipv4.zywvvd.com:33030/HexoFiles/images_matrixtime/20201219152843.png)](https://uipv4.zywvvd.com:33030/HexoFiles/images_matrixtime/20201219152843.png)

- 得到如下这段代码，这段代码直接黏贴到一个空的html文件联网即可运行。
```xml
<script src="https://cdn.geogebra.org/apps/deployggb.js"></script><div id="ggbApplet"></div><script>var parameters = {"id": "ggbApplet","width":468,"height":492,"showToolBar":true,"language":"zh",// use this instead of ggbBase64 to load a material from geogebra.org// "material_id":"RHYH3UQ8",// use this instead of ggbBase64 to load a .ggb file// "filename":"myfile.ggb","ggbBase64":"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",};// is3D=is 3D applet using 3D view, AV=Algebra View, SV=Spreadsheet View, CV=CAS View, EV2=Graphics View 2, CP=Construction Protocol, PC=Probability Calculator DA=Data Analysis, FI=Function Inspector, macro=Macrosvar views = {'is3D': 0,'AV': 0,'SV': 0,'CV': 0,'EV2': 0,'CP': 0,'PC': 0,'DA': 0,'FI': 0,'macro': 0};var applet = new GGBApplet(parameters, '5.0', views);window.onload = function() {applet.inject('ggbApplet')};applet.setPreviewImage('data:image/gif;base64,R0lGODlhAQABAAAAADs=','https://www.geogebra.org/images/GeoGebra_loading.png','https://www.geogebra.org/images/applet_play.png');</script>
```

#### 本地js解析ggbBase64信息

- 继续按照官方教程行事 [https://wiki.geogebra.org/en/Reference:GeoGebra\_App\_Parameters](https://www.zywvvd.com/pages/go.html?goUrl=https%3A%2F%2Fwiki.geogebra.org%2Fen%2FReference%3AGeoGebra_App_Parameters)
- 主要在 `Offline and Self-Hosted Solution` 这一部分
- 需要自己 [下载相关的js文件](https://www.zywvvd.com/pages/go.html?goUrl=https%3A%2F%2Fdownload.geogebra.org%2Fpackage%2Fgeogebra-math-apps-bundle) （ `deployggb.js` 和 `5.0/web3d/` ）
- 配置 `deployggb.js` 和 `5.0/web3d/` 的位置
- 我将 `deployggb.js` 放在了 `/vvd_js/deployggb.js` 下； `web3d` 放在了 `/vvd_js/5.0/web3d/` 位置
- 我将 `deployggb.js` 放在了 `/vvd_js/deployggb.js` 下； `web3d` 放在了 `/vvd_js/5.0/web3d/` 位置
- 我将 `deployggb.js` 放在了 `/vvd_js/deployggb.js` 下； `web3d` 放在了 `/vvd_js/5.0/web3d/` 位置
- 我将 `deployggb.js` 放在了 `/vvd_js/deployggb.js` 下； `web3d` 放在了 `/vvd_js/5.0/web3d/` 位置

> 此处建议放在hexo目录的source文件夹中，然后在hexo配置文件中设置skip-render来保存这些js文件，可以兼容所有主题使用

- 代数区输入公式 $y=ax+b$ 创建图形
- 为了让图形居中显示，在调用的div模块上加入style设置 `style='margin:0 auto'` ：
- 综上，在html贴上如下代码：
```xml
<script src="https://uipv4.zywvvd.com:33030/HexoFiles/js/vvd_js/deployggb.js"></script><script>var parameters = {"id": "ggbApplet","width":500,"height":500,"showResetIcon":true,"borderColor":"white","language":"en","ggbBase64":"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"};var applet = new GGBApplet(parameters, '5.0');applet.setHTML5Codebase('/vvd_js/5.0/web3d/');applet.setHTML5Codebase('/vvd_js/5.0/web3d/');window.onload = function() {applet.inject('ggbApplet')};</script><div id="ggbApplet" style='margin:0 auto'></div>
```

#### 本地js解析ggb文件信息

- 与官网解析ggb文件一样，首先获取 `ggb文件` ，将文件上传，获取链接
- 将上文的 `ggbBase64` 替换为 `filename` ，附上链接，向网页黏贴代码
```xml
<script src="{path to your deployggb.js}"></script><script>var parameters = {"id": "ggbApplet","width":500,"height":500,"borderColor":"white","language":"en","filename":"https://uipv4.zywvvd.com:33030/HexoFiles/images_matrixtime/20201219164932.ggb"};var applet = new GGBApplet(parameters, '5.0');applet.setHTML5Codebase('5.0/web3d/');window.onload = function() {applet.inject('ggbApplet')};</script><div id="ggbApplet"></div>
```

#### js解析ggb信息过程中的参数设置

- 参考： [https://wiki.geogebra.org/en/Reference:GeoGebra\_App\_Parameters](https://www.zywvvd.com/pages/go.html?goUrl=https%3A%2F%2Fwiki.geogebra.org%2Fen%2FReference%3AGeoGebra_App_Parameters)
- 可以根据个人需求设置各项参数

| Name | Value | Description | Since |
| --- | --- | --- | --- |
| appName | eg `"graphing"` | app name, default: “classic”“graphing” … GeoGebra Graphing Calculator “geometry” … GeoGebra Geometry “3d” … GeoGebra 3D Graphing Calculator “classic” … GeoGebra Classic “suite” … GeoGebra Calculator Suite “evaluator” … Equation Editor | 6.0 |
| width | eg `800` | Applet width (**compulsory field**) |  |
| height | eg `600` | Applet height (**compulsory field**) |  |
| material\_id | eg `"RHYH3UQ8"` | GeoGebra Materials id to load See first applet here: [https://dev.geogebra.org/examples/html/example-multiple.html](https://www.zywvvd.com/pages/go.html?goUrl=https%3A%2F%2Fdev.geogebra.org%2Fexamples%2Fhtml%2Fexample-multiple.html) | 5.0 |
| filename | eg `"myFile.ggb"` | URL of file to load See second applet here: [https://dev.geogebra.org/examples/html/example-multiple.html](https://www.zywvvd.com/pages/go.html?goUrl=https%3A%2F%2Fdev.geogebra.org%2Fexamples%2Fhtml%2Fexample-multiple.html) | 4.0 |
| ggbBase64 | base64 encoded.ggb file | Encoded file to load. See the applet here: [https://dev.geogebra.org/examples/html/example-single.html](https://www.zywvvd.com/pages/go.html?goUrl=https%3A%2F%2Fdev.geogebra.org%2Fexamples%2Fhtml%2Fexample-single.html) | 4.0 |
| borderColor | e.g. `#FFFFFF` for white | Color of the border line drawn around the applet panel (as hex rgb string). Default: gray | 3.0 |
| enableRightClick | `true` or `false` | States whether right clicks should be handled by the applet. Setting this parameter to “false” disables context menus, properties dialogs and right-click-zooming. Default: true. NB also enables/disables some keyboard shortcuts eg Delete and Ctrl + R (recompute all objects). Default: true | 3.0 |
| enableLabelDrags | `true` or `false` | States whether labels can be dragged. Default: true | 3.2 |
| enableShiftDragZoom | `true` or `false` | States whether the Graphics View(s) should be moveable using Shift + mouse drag (or. Ctrl + mouse drag) or zoomable using Shift + mouse wheel (or Ctrl + mouse wheel). Setting this parameter to “false” disables moving and zooming of the drawing pad. Default: true | 3.0 |
| showZoomButtons | `true` or `false` | States whether the zoom in / zoom out / home buttons should be shown in the Graphics View or not. Default: false | 6.0 |
| errorDialogsActive | `true` or `false` | States whether error dialogs will be shown if an invalid input is entered (using the Input Bar or JavaScript) Default: true | 3.2 |
| showMenuBar | `true` or `false` | States whether the menubar of GeoGebra should be shown in the applet. Default: false | 2.5 |
| showToolBar | `true` or `false` | States whether the toolbar with the construction mode buttons should be shown in the applet. Default: false | 2.5 |
| showToolBarHelp | `true` or `false` | States whether the toolbar help text right to the toolbar buttons should be shown in the applet | 3.0 |
| customToolBar | e.g. `0 1 2 3 , 4 5 6 7` | Sets the toolbar according to a custom toolbar string where the int values are [Toolbar Mode Values](https://www.zywvvd.com/pages/go.html?goUrl=https%3A%2F%2Fwiki.geogebra.org%2Fen%2FReference%3AToolbar), `,` adds a separator within a menu, \` | `starts a new menu and` |
| showAlgebraInput | `true` or `false` | States whether the algebra input line (with input field, greek letters and command list) should be shown in the applet. Default: false | 2.5 |
| showResetIcon | `true` or `false` | States whether a small icon (GeoGebra ellipse) should be shown in the upper right corner of the applet. Clicking on this icon resets the applet (i.e. it reloads the file given in the filename parameter). Default: false | 2.5 |
| language | [iso language string](https://www.zywvvd.com/pages/go.html?goUrl=http%3A%2F%2Fen.wikipedia.org%2Fwiki%2FList_of_ISO_639-1_codes) | GeoGebra tries to set your local language automatically (if it is available among the supported languages, of course). The default language for unsupported languages is English. If you want to specify a certain language manually, please use this parameter. | 2.5 |
| country | iso country string, e.g. `AT` for Austria | This parameter only makes sense if you use it together with the language parameter. | 2.5 |
| id | eg `applet2` | This parameter allows you to specify the argument passed to the JavaScript function ggbOnInit(), which is called once the applet is fully initialised. This is useful when you have multiple applets on a page - see [this example](https://www.zywvvd.com/pages/go.html?goUrl=http%3A%2F%2Fdev.geogebra.org%2Fexamples%2Fhtml%2Fexample-api-sync.html) (will have no effect in earlier versions) | 3.2 |
| allowStyleBar | `true` or `false` | Default: false Determines whether the Style Bar can be shown (or will be shown if just Graphics View 1 is showing) | 4.0 |
| appletOnLoad | eg `function(api){ api.evalCommand('Segment((1,2),(3,4))'); }` | JavaScript method to run when the activity is initialized (and file loaded if applicable) | 5.0 |
| useBrowserForJS | `true` or `false` | When true, GeoGebraruns ggbOnInit from HTMLignores ggbOnInit from fileignores JS update scripts of objects in fileWhen false, GeoGebra:ignores ggbOnInit from HTML (use appletOnLoad parameter of GGBApplet instead)runs ggbOnInit from fileruns JS update scripts of objects in file **Default: false** | 4.0 |
| showLogging | `true` or `false` | Default: false Determines whether logging is shown in the Browser’s console | 4.2 |
| capturingThreshold | integer | Default: 3 Determines the sensitivity of object selection. The default value of 3 is usually fine to select and drag objects both with the mouse and touch. Use larger values (e.g. 4 or 5) to make it easier to select and drag objects. | 4.4 |
| enableFileFeatures | `true` or `false` | Default: true Determines whether file saving, file loading, sign in and Options > Save settings are enabled. This argument is ignored when menubar is not showing. | 5.0 |
| perspective | string | For values see [SetPerspective\_Command](https://www.zywvvd.com/pages/go.html?goUrl=https%3A%2F%2Fwiki.geogebra.org%2Fen%2FSetPerspective_Command). Just for a blank start ie shouldn’t be used with *material\_id*, *filename* or *ggbBase64* parameters | 5.0 |
| enable3d | `true` or `false` or none | Whether 3D should be enabled (for exam mode). When neither true nor false are entered, user can decide in a dialog. | 5.0 |
| enableCAS | `true` or `false` or none | Whether CAS should be enabled (for exam mode). When neither true nor false are entered, user can decide in a dialog. | 5.0 |
| algebraInputPosition | `algebra`, `top` or `bottom` | Default: empty Determines whether input bar should be shown in algebra, on top of the applet or under the applet. When left empty, the position depends on file. | 5.0 |
| preventFocus | `true` or `false` | Default: false. When set to true, this prevents the applet from getting focus automatically at the start. | 5.0 |
| scaleContainerClass | String | Name of CSS class that is used as container; applet will scale to fit into the container. | 5.0 |
| autoHeight | boolean | • `true` to restrict the width of the applet and compute height automatically, add `autoHeight:true` • `false` if you want the applet to be restricted by both width and height of the container | 5.0 |
| allowUpscale | `true` or `false` | Default: false Determines whether automatic scaling may scale the applet up | 5.0 |
| playButton | `true` or `false` | Default: false Determines whether a preview image and a play button should be rendered in place of the applet. Pushing the play button initializes the applet. | 5.0 |
| scale | number | Ratio by which the applet should be scaled (eg. 2 makes the applet 2 times bigger, including all texts and UI elements). Default: 1 | 5.0 |
| showAnimationButton | `true` or `false` | Whether animation button should be visible | 5.0 |
| showFullscreenButton | `true` or `false` | Whether fullscreen button should be visible | 6.0 |
| showSuggestionButtons | `true` or `false` | Whether suggestion buttons (special points, solve) in Algebra View should be visible | 6.0 |
| showStartTooltip | `true` or `false` | Whether “Welcome” tooltip should be shown | 5.0 |
| rounding | string | String composed of number of decimal places and flags – valid flags are “s” for significant digits and “r” for rational numbers. Hence “10” means 10 decimal places, “10s” stands for 10 significant digits. | 6.0 |
| buttonShadows | `true` or `false` | Whether buttons should have shadow | 6.0 |
| buttonRounding | Number (0 - 0.9) | Relative radius of button’s rounded border. The border radius in pixels is `buttonRounding * height /2`, where `height` is the height of the button. Default 0.2. | 6.0 |
| buttonBorderColor | Hex color (`#RGB`, `#RGBA`, `#RRGGBB` or `#RRGGBBAA`) | Border color of buttons on the graphics view. Default is black, if the button background is white, otherwise one shade darker than the background color | 6.0 |
| editorBackgroundColor | Hex color | Background color of the evaluator app | 6.0 |
| editorForegroundColor | Hex color | Foreground (text) color of the equation editor (appname = “evaluator”) | 6.0 |
| textmode | false\], default false | whether editor is in text mode or not (appname = “evaluator”) | 6.0 |
| keyboardType | “normal”\|“notes”\] | Which keyboard is shown for equation editor (appname = “evaluator”) | 6.0 |

### Hexo 稳妥嵌入 geogebra 最佳实践

- 个人偏好的最佳实践路径：
- 优点：
- 自己提供服务，不受官网束缚
- 使用图形源文件提供展示，安全可靠
- 可互动，有滑块，可以满足绝大多数展示需求
- 流程相对简单清晰
- 加载速度可以接受
- 手机端可以显示同样效果
- 环境配好后无缝融入hexo博客环境

### 参考资料

- [https://www.geogebra.org/](https://www.zywvvd.com/pages/go.html?goUrl=https%3A%2F%2Fwww.geogebra.org%2F)
- [https://blog.csdn.net/fatty\_zhu/article/details/77411254](https://www.zywvvd.com/pages/go.html?goUrl=https%3A%2F%2Fblog.csdn.net%2Ffatty_zhu%2Farticle%2Fdetails%2F77411254)
- [https://www.bilibili.com/video/av80321187/](https://www.zywvvd.com/pages/go.html?goUrl=https%3A%2F%2Fwww.bilibili.com%2Fvideo%2Fav80321187%2F)
- [https://kz16.top/](https://www.zywvvd.com/pages/go.html?goUrl=https%3A%2F%2Fkz16.top%2F)
- [https://wiki.geogebra.org/en/Reference:GeoGebra\_App\_Parameters](https://www.zywvvd.com/pages/go.html?goUrl=https%3A%2F%2Fwiki.geogebra.org%2Fen%2FReference%3AGeoGebra_App_Parameters)
  
  

> 文章链接：  
> [https://www.zywvvd.com/notes/tools/geogebra/geogebra-html-embed/geogebra-html-embed/](https://www.zywvvd.com/notes/tools/geogebra/geogebra-html-embed/geogebra-html-embed/)

---

“觉得不错的话，给点打赏吧 ୧(๑•̀⌄•́๑)૭”