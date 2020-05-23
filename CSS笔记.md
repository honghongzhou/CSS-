# HTML

1. doctype的意义：让浏览器以标准模式渲染；让浏览器知道元素的合法性；

2. HTML XTML HTML5的关系：

​	HTML属于SGML的

​	XHTML属于XML，是HTML进行XML严格化的结果

​	HTML5不属于SGML和XML，比XHTML宽松

3. HTML5有什么变化

​	新的语义化元素，表单增强，新的API（离线，音视频，图形，实时通信，本地存储，设备能力），分类和嵌套变更

4. em和i有什么区别

​	em是语义化的标签，表强调

​	i是纯样式的标签，表斜体

​	HTML5中i不推荐使用，一般用作图标

5. 语义化的意义

​	开发者容易理解，机器容易理解结构（搜索，读屏软件），有助于SEO，semantic microdata

6. 哪些元素可以自闭合

​	表单元素input，图片img，br hr， meta link

7. HTML和DOM的关系

​	DOM是由HTML解析而来，JS可以维护DOM

8. property和attribute的区别

​	attribute是死的，property是活的

# CSS

## 魔鬼属性float

* 浮动的本质是为了实现文字环绕效果。主要指文字环绕图片显示的效果。

* float特性：

  * 包裹性（包裹+自适应性）
  * 块状化并格式化上下文（元素一旦float的属性值不为none，则其display计算值就是block或者table（除了inline-table计算为table外，其余都是block））
  * 破坏文档流
  * 没有任何margin合并

* 浮动带来的影响

  * 浮动元素会影响兄弟元素的位置。如果兄弟元素是块级元素，则会忽略浮动的元素，导致本身的元素被浮动元素覆盖；如果兄弟元素是内联元素，则会尽可能围绕浮动元素。
  * 浮动元素脱离了标准文档流，会导致父级元素高度塌陷。

* 清除浮动带来的影响方法
  
  * 添加空的div，或者设置overflow:hidden/auto；或者使用伪元素clear属性。

* 清除浮动影响的本质

  1. 利用clear属性，包括在浮动元素末尾添加一个带有clear:both属性的空的div来闭合元素，其实利用:after伪元素的方法也是在元素末尾添加一个内容为一个点并带有clear:both属性来实现的。（clear解释：元素盒子的边不能和前面的浮动元素相邻；clear属性只有块级元素才有效，而::after等伪元素都是内联元素，这就是借助伪元素清除浮动影响时需要设置display属性值的原因。）
  2. 触发浮动元素父元素的BFC（Block Formatting Contexts，块级格式化上下文），使得该父元素可以包含浮动元素。

## 多余的width: ，包含100%

* 默认的流体布局中，width: 100%是一种margin/border/padding和content内容区域自动分配水平空间的机制。

* 借助流动性无宽度布局，充分利用浏览器原生流动性的好处。

## CSS的包裹性

* CSS 的包裹性：包裹+自适应性

* 按钮是CSS世界中极具有代表性的inline-block元素，可谓展示“包裹性”最好的例子，具体表现为：按钮文字越多越宽（内部尺寸特性），但是如果文字足够多，则会在容器的宽度处自动换行（自适应性）。

## box-sizing

* 唯一离不开box-sizing: border-box的就是原生普通文本框<input>和文本域<textarea>的100%自适应父容器宽度。

* textarea为替换元素，替换元素的特性之一就是尺寸由内部元素决定，且无论display的属性是inline还是block。非替换元素，如果其display的属性值为block则会具有流动性，宽度由外部尺寸决定。

* 因此我们只能通过width设定<textarea>尺寸100%自适应父容器。

* 问题就是：textarea是有border的，而且需要一定的padding，否则输入的时候光标就会顶着边框，体验很不好，于是，width/border和padding注定要共存，同时整体的宽度100%自适应容器。

* box-sizing被发明的初衷：解决替换元素宽度自适应的问题。

## height: 100%

* height默认的是auto。

* 要想height:100%有效的方法有两种

     1. 设置显示的高度

    2. 使用绝对定位

      但是这两种100%也是有区别的：绝对定位的百分比是相对于padding-box的，也就是说会把padding大小	的值计算在内。非绝对定位元素，则是相对于content-box的

## Content

* content与替换元素：根据是否具有可替换内容，我们可以把元素分为替换元素和非替换元素。典型的替换元素（<img>，<object>，<video>，<iframe>， <input>， <textarea>）

  * 替换元素的特点：内容的外观不受页面上的CSS的影响；有自己的尺寸；在很多CSS属性上有自己的一套表现规则；
  * 替换元素的尺寸计算规则：CSS尺寸>HTML尺寸>固有尺寸

## Padding

* padding的百分比值：padding百分比值无论是水平方向还是垂直方向均是相对于宽度计算的。

* ol/ul列表内置 padding-left，单位是px

* 很多表单元素都内置 padding（<input><textarea><select><radio><checkbox><button>）

* padding与图形绘制： padding属性和background-clip属性配合，可以在有限的标签下实现一些CSS图形绘制效果。

* padding-top，padding-bottom，margin-top，margin-bottom对于非替换元素无效，只对替换元素有效。

## Margin

* 元素尺寸的相关概念

  * 元素尺寸： 包含padding，border，也就是元素的border-box的尺寸。在原生DOM API中写作offsetWidth和offsetHeight，有时候又称为“元素偏移尺寸”
  * 元素内部尺寸：包含padding不包含border，也就是元素的padding-box。在原生DOMAPI中写作clientWidth和clientHeight。
  * 元素外部尺寸：同时包含padding，border和margin

* 滚动容器的底部的留白使用padding是不推荐的，因为兼容性是个大问题，但是，我们可以借助margin的外部尺寸特性来实现底部留白。（只能使用子元素的margin-bottom来实现滚动容器的底部留白）

* margin的百分比值：无论是水平方向还是垂直方向都是相对于宽度计算的。

* margin合并

  * 块级元素的上边距和下边距有时会合并为单个边距，这种现象称为“margin合并”。（块级元素，垂直方向）
  * 空块级元素的合并：上下margin会合并。
  * margin合并规则：正正取大值  正负值相加 负负最负值

* margin:  auto

  * 如果一侧定值，一侧auto，则auto为剩余空间的大小
  * 如果两侧均是auto，则评分剩余空间
  * margin的初始值为0

* margin无效情形解析

  * 内联元素，垂直方向margin无效

## Border

* border: 11px solid transparent; 优雅的增加点击区域的大小。

* border实现三角形的绘制

  ```
  div {
   	width: 0;
   	border: 10px solid;
  	border-color: #f30 transparent transparent;
  } 
  ```

## 内联元素与流

* ex：是CSS中的一个相对单位，指的是小写字母x的高度（x-height）

* line-height

  * 行距 = line-height - font-size
  * 块级元素的line-height
  * line-height实现内联元素的“垂直居中” （坊间传闻：要想让单行文字垂直居中，只要设置line-height的大小和height一样高就可以了。）
    * 误区一：要让单行文字垂直居中，只需要line-height这一个属性就可以，与height一点关系都没有。
    * 误区二：行高控制文字垂直居中，不仅适用于单行，多行也是可以的。
    * 误区三：这里也只能说是近似垂直居中，并无法达到准备的垂直居中。（因为文字字形的垂直中线位置普遍要比真正的“行框盒子”的垂直中线位置低）
  * 字体不一样的时候，默认的line-height也就不一致（只要字体确定，各个浏览器下的默认line-height解析值基本上都是一样的。然而关键是不同的浏览器使用的默认中英文字体并不是一样的，并且不同操作系统的默认的字体也不是一样，换句话说，就是不同系统不同浏览器默认的line-height都有差异，因此，对line-height的默认值进行重置是势在必得。）
  * line-height:1.5  line-height:150%  line-height:1.5em 这三种最终的行高大小都是和font-size计算值，但是它们在继承上有所不同。如果使用数值作为line-height的属性值（1.5），那么所有的子元素继承的都是这个值；但是如果使用百分比或者长度值作为属性（150%/1.5em），那么所有的子元素继承的是最终的计算值。
  * 内联元素line-height的大值特性：无论内联元素line-height如何设置，最终父级元素的高度都是由数值最大的那个line-height决定的。

* vertical-align

  * vertical-align 属性值可以分为以下四类
    * 线类，如baseline(默认),top,middle,bottom
    
    * 文本类，如text-top,text-bottom
    
    * 上标下标类，如sub,super
    
    * 数值百分比类，如20px,2em,20%（相对基线上移动或者下移动）（百分比是相对于line-height的计算值计算的）
    
   * vertical-align作用得前提：只能应用于内联元素以及display值为table-cell的元素。（inline , inline-block , inline-table, table-cell , 浮动定位和绝对定位会让元素块状化，因此使用vertical-align无效）

## BFC

* BFC：block formatting context 中文为“块级格式化上下文”。

* IFC： inline formatting context中文为“内联格式化上下文”。

* 如果一个元素具有BFC，内部子元素再怎么翻江倒海，翻云覆雨，都不会影响外部的元素。所以BFC元素也可以用来清除浮动的影响。同时BFC元素是不可能发生margin重叠的，因为margin重叠会影响外部元素。

* 触发BFC的条件：

  * <html>根元素
  * float的值不为none
  * overfloat的值为auto，scroll，或hidden
  * display的值为table-cell，table-caption，和inline-block中的任何一个
  * position的值不为relative和static
    * 也就是说，只要元素符合上面任意一个条件，就无须使用clear:both属性去清除浮动的影响了。

## position: absolute

* absolute与float同时存在的时候，float属性无任何效果。

* 元素一旦position：absolute或fixed，其display计算值事block或者table。

* 可以块状格式化上下文，具有包裹性。

* 一个绝对定位的元素，没有任何left/top/right/bottom属性设置，并且其祖先元素全部都是非定位元素，其位置还是在当前位置而不是浏览窗口的左上方。（absolut是非常独立的CSS属性值，其样式和行为表现不依赖其他任何CSS属性就可以完成）（无依赖定位）

* 上述得无依赖定位常用场景：select，输入框错误提示，icon

* absolute和overflow：

  * 如果overflow不是定位元素，同时绝对定位元素和overflow容器之间也没有定位元素，则overflow无法对absolute元素进行剪裁。
  * 如果overflow的属性值不是hidden，而是auto或者scroll，即使绝对定位元素高宽比overflow元素高宽还要大，也不都会出现滚动条。

* 绝对定位的流体自适应特性。

* absolute和margin：auto：绝对定位元素的margin:auto的填充规则和普通流体元素的一模一样，唯一的区别就是，绝对定位的margin：auto居中从IE8浏览器开始支持，而普通元素的居中很早就支持了。

* relative：

  * relative相对定位元素的left/top/right/bottom的百分比值是相对于包含块计算的，而不是自身。
  * 相对定位元素同时应用对立方向定位值得时候，top/bottom同时使用，bottom无效，left/right同时使用得时候，right无效。
  * relative最小化影响原则：尽量不适用relative，如果想定位某些元素，看看能否使用“无依赖得绝对定位”；如果场景受限，一定要使用relative则该relative务必最小化。

* fixed：

  * 唯一可以限制固定定位元素得就是<html>根元素。
  * 无依赖得固定定位（与无依赖得绝对定位类似）

## CSS的层叠规则

* z-index只是CSS层叠规则中的一叶小舟。且z-index只有定位的元素（即position属性值不是static的元素）的z-index才会起作用。
