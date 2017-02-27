# css-center
16种方法实现水平居中垂直居中
##导读##

熟悉水平居中和垂直居中的方法, 不为别的, 就为用的时候能够信手拈来. 下面直接步入正题.
##水平居中##

1) 若是行内元素, 给其父元素设置 text-align:center,即可实现行内元素水平居中.
2) 若是块级元素, 该元素设置 margin:0 auto即可.
3) 若子元素包含 float:left 属性, 为了让子元素水平居中, 则可让父元素宽度设置为fit-content,并且配合margin, 作如下设置:
   ```css     
	.parent{
		width: -moz-fit-content;
		width: -webkit-fit-content;
		width:fit-content;
		margin:0 auto;
	}
```
fit-content是CSS3中给width属性新加的一个属性值,它配合margin可以轻松实现水平居中, 目前只支持Chrome 和 Firefox浏览器.

4) 使用flex布局, 可以轻松的实现水平居中, 子元素设置如下:
```css
    .son{
		display: flex;
		justify-content: center;
    }
```
5) 使用css3 盒模型, 父元素display: box;box-pack: center;如下设置:
```css
     .parent {
		display: -webkit-box;
		-webkit-box-orient: horizontal;
		-webkit-box-pack: center;
		display: -moz-box;
		-moz-box-orient: horizontal;
		-moz-box-pack: center;
		display: -o-box;
		-o-box-orient: horizontal;
		-o-box-pack: center;
		display: -ms-box;
		-ms-box-orient: horizontal;
		-ms-box-pack: center;
		display: box;
		box-orient: horizontal;
		box-pack: center;
	}
```
6) 使用CSS3中新增的transform属性, 子元素设置如下:
```css
     .son{
		position:absolute;
		left:50%;
		transform:translate(-50%,0);
	}
```
7) 使用绝对定位方式, 以及负值的margin-left, 子元素设置如下:
```css
	.son{
		position:absolute;
		width:固定;
	    left:50%;
	    margin-left:-0.5宽度;
	}
```
8) 使用绝对定位方式, 以及left:0;right:0;margin:0 auto; 子元素设置如下:
```css
	.son{
		position:absolute;
		width:固定;
		left:0;
		right:0;
		margin:0 auto;
	}
```
##垂直居中

###单行文本
1) 若元素是单行文本, 则可设置 line-height 等于父元素高度

####行内块级元素

2) 若元素是行内块级元素, 基本思想是使用display: inline-block, vertical-align: middle和一个伪元素让内容块处于容器中央.
```css
	.parent::after, .son{
		display:inline-block;
		vertical-align:middle;
	}
	.parent::after{
		content:'';
		height:100%;
	}
```
这是一种很流行的方法, 也适应IE7.

###元素高度不定

3) 可用 vertical-align 属性, 而vertical-align只有在父层为 td 或者 th 时, 才会生效, 对于其他块级元素, 例如 div、p 等, 默认情况是不支持的. 为了使用vertical-align, 我们需要设置父元素display:table, 子元素 display:table-cell;vertical-align:middle;

####优点
元素高度可以动态改变, 不需再CSS中定义, 如果父元素没有足够空间时, 该元素内容也不会被截断.
####缺点
IE6~7, 甚至IE8 beta中无效.

4) 可用 Flex, 这是CSS布局未来的趋势. Flexbox是CSS3新增属性, 设计初衷是为了解决像垂直居中这样的常见布局问题. 相关的文章如[《Centering Elements with Flexbox》](http://coding.smashingmagazine.com/2013/05/22/centering-elements-with-flexbox/)

父元素做如下设置即可保证子元素垂直居中:
```css
	.parent {
	  display: flex;
	  align-items: center;
	}
```
###优点
* 内容块的宽高任意, 优雅的溢出.
* 可用于更复杂高级的布局技术中.

###缺点
* IE8/IE9不支持
* 需要浏览器厂商前缀
* 渲染上可能会有一些问题

5) 使用CSS3盒模型
```css
	.parent {
	  	display: box;
	  	box-orient: vertical;
	  	box-pack: center;
	}	
```
###优点
* 实现简单, 扩展性强
###缺点
* 兼容性差, 不支持IE

6) 可用 transform , 设置父元素相对定位(position:relative), 子元素如下css样式:
```css
	.son{
		position:absolute;
		top:50%;
		-webkit-transform: translate(-50%,-50%);  
		-ms-transform: translate(-50%,-50%);
		transform: translate(-50%,-50%);
	}
```

###优点
* 代码量少
###缺点
* IE8不支持, 属性需要追加浏览器厂商前缀, 可能干扰其他 transform 效果, 某些情形下会出现文本或元素边界渲染模糊的现象.
元素高度固定

####元素高度固定

7) 设置父元素相对定位(position:relative), 子元素如下css样式:
```css
	.son{
		position:absolute;
		top:50%;
		height:固定;
		margin-top:-0.5高度;
	}
```
###优点
* 适用于所有浏览器.
###缺点
* 父元素空间不够时, 子元素可能不可见(当浏览器窗口缩小时,滚动条不出现时).如果子元素设置了overflow:auto, 则高度不够时, 会出现滚动条.

8) 设置父元素相对定位(position:relative), 子元素如下css样式:
```css
	.son{
		position:absolute;
		height:固定;
		top:0;
		bottom:0;
		margin:auto 0;
	}
```
###优点
* 简单
###缺点
* 没有足够空间时, 子元素会被截断, 但不会有滚动条.

##总结
水平居中较为简单, 共提供了8种方法, 一般情况下 text-align:center,marin:0 auto; 足矣

* ① text-align:center;
* ② margin:0 auto;
* ③ width:fit-content;
* ④ flex
* ⑤ 盒模型
* ⑥ transform　
* ⑦ ⑧两种不同的绝对定位方法

###垂直居中, 共提供了8种方法.

* ① 单行文本, line-height
* ② 行内块级元素, 使用 display: inline-block, vertical-align: middle; 加上伪元素辅助实现
* ③ vertical-align
* ④ flex
* ⑤ 盒模型
* ⑥ transform
* ⑦ ⑧ 两种不同的绝对定位方法

我们发现, flex, 盒模型, transform, 绝对定位, 这几种方法同时适用于水平居中和垂直居中.
　　
