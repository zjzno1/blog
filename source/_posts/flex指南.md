title: flex指南
date: 2019-07-18 15:51:41
tags:
- flex
---

flex,即‘弹性布局’，任何盒模型都可以用

    .box {
        display: flex;
    }

行内元素也可以使用 Flex 布局

    .box {
        display: inline-flex;
    }

Webkit 内核的浏览器，需要加上`-webkit`（兼容ios8）

    .box{
        display: -webkit-flex; /* Safari */
        display: flex;
    }

flex有两条轴，分别是主轴（水平轴 main axis）和交叉轴（竖直轴 cross axis）;

#### 容器的属性

1) flex-direction 决定主轴的方向

值
- row // 主轴为水平方向，起点在左端
- row-reverse // 主轴为水平方向，起点在右端
- column // 主轴为垂直方向，起点在上沿
- column-reverse // 主轴为垂直方向，起点在下沿

2) flex-warp 如果一条轴线排不下，如何换行

值
- nowrap // 不换行(默认)
- wrap // 换行，第一行在上方
- wrap-reverse // 换行，第一行在下方

3) flex-flow 属性是`flex-direction`属性和`flex-wrap`属性的简写形式，默认值为`row nowrap`

值

    .box {
        flex-flow: <flex-direction> || <flex-wrap>;
    }

4) justify-content 属性定义了项目在主轴上的对齐方式

值
- flex-start 靠左对齐
- flex-end 靠右对齐
- center 居中
- space-between 均匀的间隔，（两头不留空隙）
- space-around 均匀的间隔，两头留空隙，项目之间的间隔比项目与边框的间隔大一倍

5) align-items 交叉轴上如何对齐

值
- flex-start 靠上对齐
- flex-end 靠下对齐
- center 居中
- baseline 项目的第一行文字的基线对齐
- stretch （默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度。

6) align-content 属性定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。

值
- flex-start 与交叉轴的起点对齐
- flex-end 与交叉轴的终点对齐
- center 与交叉轴的中点对齐
- space-between 与交叉轴两端对齐，轴线之间的间隔平均分布
- space-around 每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
- stretch （默认值）：轴线占满整个交叉轴。

#### 项目的属性(里面的item)

1) order 属性定义项目的排列顺序。数值越小，排列越靠前，默认为0

    .item {
        order: <integer>;
    }
2) flex-grow 属性定义项目的放大比例，默认为0，即如果存在剩余空间，也不放大。

3) flex-shrink 属性定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小 （如果一个项目的flex-shrink属性为0，其他项目都为1，则空间不足时，前者不缩小。）
4) flex-basis 属性定义了在分配多余空间之前，项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为auto，即项目的本来大小
5) flex 属性是flex-grow（元素水平方向在哪，越小越靠前）, flex-shrink （元素等比缩小）和 flex-basis（元素的宽度）的简写，默认值为0 1 auto。后两个属性可选。
6) align-self 属性允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性。默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch。

