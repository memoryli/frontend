# frontend
# 前端面试宝典
# Html相关
## 1 html语义化
意义：根据内容的结构化（内容语义化），选择合适的标签（代码语义化）便于开发者阅读和写出更优雅的代码的同时让浏览器的爬虫和机器很好地解析。注意：<br>
1.尽可能少的使用无语义的标签div和span；<br>
2.在语义不明显时，既可以使用div或者p时，尽量用p, 因为p在默认情况下有上下间距，对兼容特殊终端有利；<br>
3.不要使用纯样式标签，如：b、font、u等，改用css设置。<br>
4.需要强调的文本，可以包含在strong或者em标签中（浏览器预设样式，能用CSS指定就不用他们），strong默认样式是加粗（不要用b），em是斜体（不用i）；<br>
5.使用表格时，标题要用caption，表头用thead，主体部分用tbody包围，尾部用tfoot包围。表头和一般单元格要区分开，表头用th，单元格用td；<br>
6.表单域要用fieldset标签包起来，并用legend标签说明表单的用途；<br>
7.每个input标签对应的说明文本都需要使用label标签，并且通过为input设置id属性，在lable标签中设置for=someld来让说明文本和相对应的input关联起来。<br>
# CSS相关
## 1.盒模型
盒模型是有两种标准的，一个是标准模型，一个是IE模型。<br>
标准模型中，盒模型的宽高只是内容（content）的宽高<br>
IE模型中盒模型的宽高是内容(content)+填充(padding)+边框(border)的总宽高。<br>
box-sizing属性介绍<br>
box-sizing : content-box|border-box|inherit;<br>
content-box ,默认值，可以使设置的宽度和高度值应用到元素的内容框。盒子的width只包含内容。<br>
border-box , 设置的width值其实是除margin外的border+padding+element的总宽度<br>
两种盒模型的相互转换<br>
box-sizing: content-box 是W3C盒子模型 <br>
box-sizing: border-box 是IE盒子模型<br>
再来说一说边距重叠的问题<br>
边界重叠是指两个或多个盒子(可能相邻也可能嵌套)的相邻边界(其间没有任何非空内容、补白、边框)重合在一起而形成一个单一边界。<br>
两个或多个块级盒子的垂直相邻边界会重合，它们的边界宽度是相邻边界宽度中的最大值。注意水平边界是不会重合的。<br>
边距重叠例子<br>
父子元素的边界重叠<br>
```
<style>
    .parent {
        background: #E7A1C5;
    }
    .parent .child {
        background: #C8CDF5;
        height: 100px;
        margin-top: 10px;
    }
</style>
<section class="parent">
    <article class="child"></article>
</section>
```
在这里父元素的高度不是110px，而是100px，在这里发生了高度坍塌。原因是如果块元素的 margin-top 与它的第一个子元素的margin-top 之间没有 border、padding、inline content、 clearance 来分隔，或者块元素的 margin-bottom 与它的最后一个子元素的margin-bottom 之间没有 border、padding、inline content、height、min-height、 max-height 分隔，那么外边距会塌陷。子元素多余的外边距会被父元素的外边距截断。<br>
兄弟元素的边界重叠<br>
```
<style>
    #margin {
        background: #E7A1C5;
        overflow: hidden;
        width: 300px;
    }
    #margin>p {
        background: #C8CDF5;
        margin: 20px auto 30px;
    }
</style>
<section id="margin">
    <p>1</p>
    <p>2</p>
    <p>3</p>
</section>
```
可以看到1和2,2和3之间的间距不是50px，发生了边距重叠是取了它们之间的最大值30px。<br>
空元素的边界重叠<br>
假设有一个空元素，它有外边距，但是没有边框或填充。在这种情况下，上外边距与下外边距就碰到了一起，它们会发生合并：<br>

BFC原理<br>
解决上述问题的其中一个办法就是创建BFC。BFC的全称为Block Formatting Context，即块级格式化上下文。一个BFC有如下特性：<br>
处于同一个BFC中的元素相互影响，可能会发生margin collapse；<br>
BFC在页面上是一个独立的容器，容器里面的子元素不会影响到外面的元素，反之亦然；<br>
计算BFC的高度时，考虑BFC所包含的所有元素，包括浮动元素也参与计算；<br>
浮动盒的区域不会叠加到BFC上；<br>
创建BFC的方法如下：<br>
浮动（float的值不为none）；<br>
绝对定位元素（position的值为absolute或fixed）；<br>
行内块（display为inline-block）
表格单元（display为table、table-cell、table-caption等HTML表格相关属性）；<br>
弹性盒（display为flex或inline-flex）；<br>
overflow不为visible；<br>
## 2、几种获得宽高的方式
dom.style.width/height   这种方式只能取到dom元素内联样式所设置的宽高，也就是说如果该节点的样式是在style标签中或外联的CSS文件中设置的话，通过这种方法是获取不到dom的宽高的。<br>
## 3、css reset 和 normalize.css 有什么区别
两者都是通过重置样式，保持浏览器样式的一致性<br>
前者几乎为所有标签添加了样式，后者保持了许多浏览器样式，保持尽可能的一致<br>
后者修复了常见的桌面端和移动端浏览器的bug：包含了HTML5元素的显示设置、预格式化文字的font-size问题、在IE9中SVG的溢出、许多出现在各浏览器和操作系统中的与表单相关的bug。<br>
前者中含有大段的继承链<br>
后者模块化，文档较前者来说丰富<br>
## 4、实现水平垂直居中的方式
### 1、absolute + 负margin（我称其为拉回方式）
```
    position: absolute;;
    top: 50%;
    left: 50%;
    margin-left: -50px;
    margin-top: -50px;
```
这种方式比较好理解，兼容性也很好，缺点是需要知道子元素的宽高
### 2、absolute + margin auto
```
    position: absolute;;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    margin: auto;
```
这种方法兼容性也很好，缺点是需要知道子元素的宽高
### 3、absolute + calc
```
position: absolute;;
top: calc(50% - 50px);
left: calc(50% - 50px);
```
这种方式的缺点也是需要知道子元素的宽高
### 4、absolute + transform
```
position: absolute;
top: 50%;
left: 50%;
transform: translate(-50%, -50%)
```
### 5、line-height text-align
### 6、writing-mode
```
<div class="wp">
    <div class="wp-inner">
        <div class="box">123123</div>
    </div>
</div>
/* 定位代码 */
.wp {
    writing-mode: vertical-lr;
    text-align: center;
}
.wp-inner {
    writing-mode: horizontal-tb;
    display: inline-block;
    text-align: center;
    width: 100%;
}
.box {
    display: inline-block;
    margin: auto;
    text-align: left;
}
```
### 7、table
tabel单元格中的内容天然就是垂直居中的，只要添加一个水平居中属性就好了
### 8、table-cell
```
display: table-cell;
text-align: center;
vertical-align: middle;
```
### 9、flex
```
display: flex;
justify-content: center;
align-items: center;
```
### 10、grid
```
<div class="wp">
    <div class="box">123123</div>
</div>
.wp {
    display: grid;
}
.box {
    align-self: center;
    justify-self: center;
}
```
## 
# Javascript























