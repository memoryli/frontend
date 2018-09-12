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
假设有一个空元素，它有外边距，但是没有边框或填充。在这种情况下，上外边距与下外边距就碰到了一起，它们会发生合并：
