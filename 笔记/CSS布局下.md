# CSS定位
盒模型：  
* 背景色的范围是border外边沿围成的区域
* div分层：从下到上，backgroud border 块级子元素 浮动元素 内联子元素 定位元素(z-index决定层级)，如果z-index小于0就会到backgroud下面，大于0就在最上面
  
## position
* static 默认值 当前文档流中元素的位置
* relative 文档流中占的位置不变 只是显示的位置变了。场景：对位置 配合absolute使用
* absolute 绝对定位 脱离原来的位置，最近的祖先元素需要有定位元素（不是static元素），最好把top/left也写上
* 默认每个元素的z-index是auto 
* white-space:nowrap 文字不换行
* 如何把hover元素展示出来：F12选择元素，然后styles里面选择:hov把：hover勾上
* fixed 固定定位，相对于视口定位，用了transform属性会影响，手机上不要用
* sticky 适合导航标题，兼容不好 粘滞定位
## 层叠上下文
* 同一个作用于的z-index才能比较 
```html
*{
  margin:0;
  padding:0;
  box-sizing:border-box;
}
.a{
  position:relative;
  z-index:12
}
.a>.a1{
  position:relative;
  width:100px;
  height:100px;
  background-color: red;
  z-index:10;
  top:50px;
}
.b{
  position: relative;
}
.b>.b1{
  position:relative;
  width:100px;
  height: 100px;
  background: green;
  z-index:11;
}
```
### 创建层叠上下文
*  文档根元素（<html>）；
*  position 值为 absolute（绝对定位）或  relative（相对定位）且 z-index 值不为 auto 的元素；
*  position 值为 fixed（固定定位）或 sticky（粘滞定位）的元素（沾滞定位适配所有移动设备上的浏览器，但老的桌面浏览器不支持）；
*  flex (flexbox (en-US)) 容器的子元素，且 z-index 值不为 auto；
*  grid (grid) 容器的子元素，且 z-index 值不为 auto；
*  opacity 属性值小于 1 的元素（参见 the specification for opacity）；
*  mix-blend-mode 属性值不为 normal 的元素；
*  以下任意属性值不为 none 的元素：
transform
filter
perspective
clip-path
mask / mask-image / mask-border
*  isolation 属性值为 isolate 的元素；
*  -webkit-overflow-scrolling 属性值为 touch 的元素；
*  will-change 值设定了任一属性而该属性在 non-initial 值时会创建层叠上下文的元素（参考这篇文章）；
*  contain 属性值为 layout、paint 或包含它们其中之一的合成值（比如 contain: strict、contain: content）的元素。
* z-index/flex/opacity/transform记住就行了