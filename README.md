Chopper
==================

简单易用的前端样式解决方案。

目录
================

*   [概述](#overview)
    *   [背景](#background)
*   [规范](#standard)
    *   [模块组织规范](#organize)
    *   [模块命名规范](#classname)
    *   [代码注释规范](#note)
    *   [组件规范](#component)
        *    [构建](component-structure)
        *    [维护](component-maintain)
        *    [升级](component-upgrade)
*   [感谢](#acknowledgement)

<h2 id="overview">概述</h2>

<h3 id="background">背景</h3>

Chopper是theCN.com的一套样式解决方案。在CN V3版本第二次进行样式更新时，愈发的感觉到样式模块化的价值和意义重大，因此基于原有的样式表进行重构，参考国内外几大CSS框架进行自己的样式框架化构建。

因为源码是基于原有的样式表，因此存在一些历史遗留的问题。这部分代码将在接下来被修正。

<h2 id="standard">规范</h2>

<h3 id="organize">模块组织规范</h3>

1. 基础框架
    * 样式重设: base.css 浏览器重设样式，它扫除了浏览器默认样式的基本兼容性问题。
    * 全局设置：global.css 针对项目的特殊性，进行一些全局样式的设置(body, a , input...)
    * 常用功能类：common.css 提供一些常用的样式类
    * 栅格系统：grid.css 布局样式类
2. 通用模块
    * 组件类：可复用的组件，包括按钮button.css、列表list.css、盒子箱box.css等功能
3. 页面样式

<h3 id="classname">模块命名规范</h3>

```css
.ui-name /* 组件名 */
.ui-name-status /* 组件状态 */
.ui-name-content /* 组件模块 */
.ui-name-content-status /* 模块状态 */

/* 例子 */
.ui-box{}
.ui-box-head{} /* head是一个组件模块 */
.ui-box-head-title{} /* 对应的title是head的一个模块 */
.ui-box-head-border{} /* border是head一种新的状态 */

.ui-box-colorful{} /* colorful是box一种新的状态 */
.ui-box-colorful .ui-box-head{} /* 这种状态下box具备不同的head */

/*
 * 问题来了：
 * 如何区分状态和模块？哪个是状态哪个是模块？
 * 请看下面的分析和推荐
 */
```

常见的模块名

```html
head->title->text
container->content->box
list->item->text
body->wrap->main
```

神马？三层还不够用？或许是时候检查一下是否嵌套等级过深了。[《这样去写你的 HTML》](http://sofish.de/1688) [《WEB标准系列-HTML元素嵌套》](http://www.smallni.com/element-nesting/)

<h3 id="note">代码注释规范</h3>

如你上面所见的，我们把css注释分为四种：

1. 单行注释
2. 多行注释
3. 块注释
4. 代码注释

__单行注释：__

```css
/* 这是一个单行注释，注意前后空一个空格 */
```

__多行注释：__

```css
/*
 * 这是一个多行注释
 * 注释第一行是空行，第二行开始空一格，*后再空一格然后写内容
 */
```

__块注释：__

有时候一个css文件内有多个代码块功能，则需要用到块注释将它们包裹起来。（@todo 事实上一个css文件应只允许包含一个功能块。因尽可能地去拆分文件，正确css功能文件粒度最小化。）

```css
/**! block ui-box **/
.ui-box{
    
}
.ui-box-head{
    
}
/**! endblock ui-box **/

/**! block ui-list **/
.ui-list{
    
}
.ui-list-item{
    
}
/**! endblock ui-list **/
```

__代码注释：__

有时候我们需要临时屏蔽某部分代码，则需要用到代码注释。

```css
.ui-list{
    /*width: 52%;*/
    margin-left: 2%;
}
/*.ui-list-item{
    float: left;
}*/

/* 应注意到代码注释和单行注释的不同。单行注释前后需空格。 */
```

<h3 id="component">组件规范</h3>

<h4 id="component-structure">构建</div>

如何开发一个新的组件？

首先确保你已经安装了node.js, npm, [spm](https://github.com/spmjs/spm/wiki)（前端包管理工具）, [nico](http://lab.lepture.com/nico/zh/)（静态文档生成工具）.

```shell
#安装chopper初始化工具
curl https://raw.github.com/chopper-UI/spm-init/master/boot.sh | sh

#安装chopper theme(用于生成文档)
curl https://raw.github.com/chopper-UI/spm-theme/master/boot.sh | sh

#新建一个组件
mkdir box
spm init chopper
cd src
vim box.css
cd ..
vim README.md

#构建
make build-doc

#发布：目前这一步还得手动，节操尽失。
```

<h2 id="acknowledgement">感谢</h2>

* [Alice - 支付宝的样式解决方案](http://aliceui.org/)
* [Bootstrap中文网](http://www.bootcss.com/)
