# CSS总结
## 学了几天的css，今天来总结下学过的css知识。
## css两种语句类型
第一种是由选择器+属性键值对的方式.属性是一个标识符，用可读的名称来表示其特性。值则描述了浏览器引擎如何处理该特性。每个属性都包含一个有效值的集合，它有正式的语法和语义定义，被浏览器引擎实现。   
```html
.div{
	width:100px;
	height:100px;
	margin: 10px 10px;
	padding: 20px 20px;
}
```
第二种是at规则（at-rules），以*@*符号开始，随后是标识符，一直到以分号或右大括号结束。at规则涵盖了meta信息（比如 @charset  @import)，条件信息（比如@media  @document), 描述信息（比如@font-face)。  
```html
@charset 'utf-8'; 用来定义CSS文件的编码，如果文件中有中文可以正常显示出来，如果中文显示乱码可以在文件顶部加上这个声明
@import "mystyle.css";用来引入CSS的文件内容，除了@charset 'utf-8'外都引入
@media 媒体查询，它可以针对不同的屏幕尺寸设置不同的样式，一般用于响应式的页面
@keyframes 用来定义动画关键帧


@keyframes heart {
            0% {
                transform: scale(1.0);
            }

            50% {
                transform: scale(1.5);
            }

            100% {
                transform: scale(1.0);
            }
}
```

## 调试方法
布局的时候，给调试的元素加上border属性，这样就可以很清楚的看到元素的布局~另外Chrome的开发者工具调试也很好用


## 选择器使用
* 类选择器:class元素可以有多个值，中间用空格隔开。一个文件中，可以有多个相同的class。
```html
.box{
	border : 1px solid red;
}

<div class="box center">这是用了class</div>
```
* ID选择器：#号加上id名称组成。但是单个文件中id值要保持唯一。一个元素中只能设置一个id值
```html
#main{
	margin:0;
	padding:0;
	background-color: #ccc;
}
<div id="main">这是主体</div>
```


* 通用选择器：* 号代表一个页面的所有元素。一般用来做reset用，可以copy一些公司的reset.css
```html
*{
	margin:0;
	padding:0;
	font-size:15px;
}
```
* 伪类选择器：以:作为前缀，被添加到一个选择器末尾的关键字。在特定状态下会把样式加到元素上，可以往元素的选择器后面加上伪类。
```html
demo{
	width:100px;
	height:100px;
}
demo:hover{
	width:250px;
	height:250px;
}
li:nth-child(1){
	border:1px solid red;
}
```


* 伪元素选择器：通过::这样两个冒号前缀，组合关键字，添加到某个元素的后面，去选择该元素的某个部分，比如清除浮动用的
```html
.clearfix::after{
	content:'';
	display:block;
	clear:both;
}
```
* 组合选择

* 选择器组	A,B	匹配A或B的任意元素 ，或者匹配A和B
* 后代选择器	A B	B是A的后代节点,匹配B
* 子选择器	A>B	B是A的直接子节点,匹配B
* 相邻兄弟选择器	A+B	B是A的下一个兄弟节点，B紧跟A，匹配B
* 通用兄弟选择器	A~B	B是A之后的兄弟节点中的任一个，匹配B


## 两种盒模型（一般border-box用的较多）
```html
box-sizing: content-box; 内容盒模型（默认值）
.box1{
	box-sizing:content-box;
}

.box2{
	box-sizing:border-box;
}

box-sizing: border-box; 边框盒模型
```
* 两者的主要区别是盒子宽高是否包括元素的边框和内边距
* content-box的width=内容的宽度
* border-box 的width=内容的宽度 + padding + border


## 文档流和脱离文档流
* 文档流
> 简单来说标准流就是浏览器按照各种元素标签排版布局中默认的状态，浏览器在渲染代码的时候是从左往右、从上到下开始渲染，元素也是从左往右、从上往下的流式排列。也就是没有被其他排版浮动和定位相关的CSS属性干扰的就叫标准流。
* 脱离文档流（浮动、绝对定位、固定定位会脱离文档流）
> 1、如果元素不再满足浏览器的默认布局排版，也就是说将元素从默认的布局排版中拿走，此时这个元素不再占有它在标准流中的位置。那么这时这个元素就脱离了文档标准流，此时就是脱离文档流了。<br>
2、元素脱离文档流之后，将不再在文档流中占据空间，而是处于浮动状态（可以理解为漂浮在文档流的上方）。<br>
3、脱离文档流的元素的定位基于正常的文档流，当一个元素脱离文档流后，依然在文档流中的其他元素将忽略该元素并填补其原先的空间。<br>


## loat布局、flex布局、grid布局
### float布局
* 这个布局专门为IE做的，现在用的比较少了
* 步骤：
	* 子元素加float:left和width
	* 在父元素加.clearfix
```html
	.clearfix::after{
		content:'';
		display:block;
		clear:both;
	}
```
### flex布局
* flex布局是通过修改父div的display属性，让父元素成为一个flex容器，从而可以自由的操作容器中子元素(项目)的排列方式
```html
.container{
	display:flex;
}
或者
.container{
	display:inline-flex;
}
```


* flex布局属性主要由容器属性和项目属性构成(container和items)
* 容器的属性
1. flex-direction:用于控制项目排列方向与顺序,取值 row(默认) | row-reverse | column | column-reverse
2. flex-wrap:用于控制项目是否换行，nowrap表示不换行 取值 nowrap(默认) | wrap | wrap-reverse
3. flex-flow:flex-flow属性是flex-deriction与flex-wrap属性的简写集合，默认属性为row nowrap，即横向排列不换行，一般使用优先使用这个
4. justify-content：用于控制项目在横轴的对齐方式，默认flex-start左对齐，center为居中，对应的flex-end为右对齐。取值：flex-start(默认) | flex-end | center | space-between | space-around | space-evenly;


5. align-items：用于控制项目在纵轴排列方式，默认stretch即如果项目没设置高度，或高度为auto，则占满整个容器。取值：flex-start | flex-end | center | baseline | stretch(默认)
6.align-content：用于控制多行项目的对齐方式，如果项目只有一行则不会起作用；默认stretch，即在项目没设置高度，或高度为auto情况下让项目填满整个容器，与align-items类似。取值：flex-start | flex-end | center | space-between | space-around | space-evenly | stretch(默认);


* 项目的属性
1. order:用于决定项目排列顺序，数值越小，项目排列越靠前。取值：默认0
2. flex-grow:用于决定项目在有剩余空间的情况下是否放大，默认不放大；即便设置了固定宽度，也会放大。取值：默认0
3. flex-shrink:用于决定项目在空间不足时是否缩小，默认项目都是1，即空间不足时大家一起等比缩小；即便设置了固定宽度，也会缩小。取值：默认1


4. flex-basis：用于设置项目宽度，默认auto时，项目会保持默认宽度，或者以width为自身的宽度，但如果设置了flex-basis，权重会width属性高，因此会覆盖widtn属性。取值：默认auto
5. flex:是flex-grow，flex-shrink与flex-basis三个属性的简写，用于定义项目放大，缩小与宽度。取值：默认0 1 auto
6. align-self:用于让个别项目拥有与其它项目不同的对齐方式，各值的表现与父容器的align-items属性完全一致


### grid布局
* grid布局是把container元素变成一个grid(网格)，只要把其display设置为grid，主要的作用是指定项目所在的网格
```html
.container{
	display:grid;
}
或者
.container{
	display:inline-grid;
}
```


* 容器属性
1. grid-template-columns / grid-template-rows :使用以空格分隔的多个值来定义网格的列和行
	* 轨道大小 track-size： 可以使用css长度（px、em等）、百分比、或用分数（用 fr 单位）
	* 网格线名字 line-name：可以选择任何名字
2. grid-template-areas :通过引用 grid-area 属性指定的 网格区域(Grid Area) 名称来定义网格模板
```html
.container {
  grid-template-areas: 
    "head head  head"
    "main main sidebar"
    "foot foot foot";
}
```


3. grid-gap:是grid-column-gap / grid-row-gap的缩写，指定网格线的大小，可以想象为设置列/行之间间距的宽度。取值为：长度值
4. justify-items：沿着行轴对齐网格内的内容
```html
.container {
  justify-items: start | end | center | stretch;
}
```
5. align-items:沿着列对齐网格内的内容
```html
.container {
  align-items: start | end | center | stretch;
}
```


## 定位
### relative，absolute，fixed的区别
绝对定位和浮动都会产生包裹性。block元素不指定width的话，默认是100%，一旦让该div浮动起来，立刻会像inline元素一样产生包裹性，宽度会跟随内容自适应。（这也是通常float元素需要手动指定width的原因）
* relative：生成相对定位的元素，相对于其正常位置进行定位
  1. 元素的位置通过left、right、top、button属性进行规定， 可以通过z-index进行层次分级
  2. 元素仍保持其未定位前的形状，原本所占的空间仍将保留。
  3. 如果没有定位偏移量，对元素本身没有任何影响


* absolute：生成绝对定位元素。使元素脱离文档流
  1. 元素原先在正常文档流中所占的空间会被后面元素占据
  2. 元素定位后生成一个块级框，而不论原来它在正常流中生成何种类型的框
  3. 设置了absolute一定要设置left或者top，否则他就按照文档流的默认位置(auto)，若同时设置top/bottom或者left/right，那么只有top或者left有效
  4. 绝对定位元素的包含块由离它最近的 ‘position’ 属性为 ‘absolute’、’relative’ 或者 ‘fixed’ 的祖先元素创建。只要父级元素设置了position并且不是static（默认既是static），那么设定了absolute的子元素即以此为包含块（最近的）。如果都没有定义，那么就相对于整个文档body定位
  5. 相对定位一般都是配合绝对定位元素使用


## transition transform animation
### tansition 过度
* tansition是一个过渡属性，就是一个属性从一个值过渡到另一个值
* transition-property：这只属性是用来指定元素中哪一个属性执行过渡效果，取值有: none all 具体某个属性 
* transiton-duration：用来指定元素转换过程的持续时间，单位为s或ms，可以作用域任何元素。默认值为0
* transition-timing-function：用来指定改变属性值的变换速率。取值有：ease（逐渐变慢）| linear（匀速）| ease-in（加速）| ease-out（减速）| ease-in-out（加速然后减速）| * * cubic-bezier（允许自定义一个时间曲线）
* transition-delay：用来指定一个动画开始执行的时间，也就是说当改变元素属性值后多唱时间执行transition效果。


### transform 变换
* translate(x,y):x轴和y轴同时移动（如果这里只设定一个值，证明x的值和y的值相同，同样的也是x轴和y轴同时移动），translateX(x),沿着x轴移动，translateY(y),沿着y轴移动。
* scale(1.5):缩放。缩放基数就是1（也就是参数是相对于1的多少倍），如果参数大于1元素就放大，反之元素就缩小。
* rotate（* deg）：围绕中心点2D旋转若干度，单位为deg(就是度)


* fixed：生成固定定位元素，相对于浏览器窗口(viewport)的定位。通常配合z-index一起来使用。像网页上的右下角的回到顶部按钮一般就是fixed定位



### animation 动画
animation是通过关键帧@keyframes来实现更为复杂的动画效果。 每个百分号属性指定了动画进度的关键帧。
```html
@keyframes heart {
	0%{
		transform: scale(1)
	}
	50%{
		transform: scale(1.5)
	}
	100%{
		transform: scale(1)
	}
} 
```
1. animation-name: 规定需要绑定到选择器的 keyframe 名称。
2. animation-duration: 规定完成动画所花费的时间，以秒或毫秒计(1s 或1000ms)
3. animation-timing-function: 规定动画的速度曲线。(默认为ease)，取值有：linear | ease | ease-in | ease-out | ease-in-out |cubic-bezier(n,n,n,n)
4. animation-delay: 规定在动画开始之前的延迟时间，以秒或毫秒计(1s 或1000ms)(默认值为0)
5. animation-iteration-count: 规定动画应该播放的次数。(默认值为1)取值有：n | infinite(无限次播放，像loadding动画就用了这个) 
6. animation-direction: 规定是否应该轮流反向播放动画。(默认值为normal) 取值有：normal|reverse|alternate|alternate-reverse|initial|inherit

## 浏览器渲染原理

1. 浏览器会将HTML解析成一个DOM树，DOM 树的构建过程是一个深度遍历过程：当前节点的所有子节点都构建好后才会去构建当前节点的下一个兄弟节。
2. 将CSS解析成 CSS Rule Tree
3. 根据DOM树和CSSOM来构造 Rendering Tree。注意：Rendering Tree 渲染树并不等同于 DOM 树，因为一些像Header或display:none的东西就没必要放在渲染树中了
4. (Layout)有了Render Tree，浏览器已经能知道网页中有哪些节点、各个节点的CSS定义以及他们的从属关系。下一步操作称之为layout，顾名思义就是计算出每个节点在屏幕中的位置
5. (Paint)再下一步就是绘制，即遍历render树，并使用UI后端层绘制每个节点
6. (Compose)合成，根据层叠关系展示画面
