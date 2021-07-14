## 布局分类
固定宽度布局：一般宽度为960/1000/1024px
不固定宽度布局:靠文档流的原理布局
响应式布局：PC上固定，手机上不固定  
## 布局思路
* 先定下大局，再完善部分的小布局
* 先完成小布局，再组合成大布局（新手推荐）
## 小技巧
1.img的下面有额外的空隙要加上:
```html
img{
    vertical-align:middle;
}
```
2.flex左右布局时，使用margin-left:auto也能使右边元素跑到右边  
3.负margin还是有点不明白？？
## 用什么布局？
布局选择
## float布局
1.在子元素上加float  
2.在父元素上加.clearfix，直接记下来
```html
.clearfix:after{
    content:'';
    display:block;
    clear:both
}
```
3.float会让元素脱离文档流  
4.float一般用在IE上，手机上不需要  
5.IE6/7存在双倍的margin,把margin减半或家还是那个display:inline-block  
6.有时候border会干扰布局，换成outline就好了  
如何让一个固定宽度的块级元素居中：加让margin-left:auto margin-right:auto  

平均布局需要在Items元素上加一层div，给div加上一个负margin  

## flex布局
教程 CSS trick  
有两个部分：container items，在container上加上display:flex  
```html
.container{
    display:flex;
    flex-direction:row | row-reverse|colum|column-reverse;
}
```
### container上的属性：  
flex-direction 主轴方向
* row 从左往右
* row-reverse 从右往左
* column 从上往下
* column-reverse 从下往上

flex-wrap 控制换行
* nowrap 不折行（会全部挤在一行，items宽度也会被改变）
* wrap 折行
* wrap-reverse  从下往上折行

justify-content 主轴对齐方式
* flex-start 往左靠
* flex-end 往右靠
* center 往中间靠
* space-between 中间距离一样隔开
* space-around 左右中间隔开 左右是中间的一半
* space-evenly 左右中间隔开 距离一样

align-items 次轴对齐方式（items高度不一致）
* flex-start 往上对齐
* flex-end 往下对齐
* center 往中间对齐
* stretch 高度拉成以最高的元素一样
* baseline 不了解

align-content 多行内容
* flex-start 往上对齐
* flex-end 往下对齐
* center 往中间对齐
* stretch 平均分
* space-between 把空出来的空间平均分
* space-around 围绕方式，也是平均分
  
### items上的属性

order items的顺序，从小到大排序  
flex-grow 控制items的空间，越大胖的越多
flex-shrink 控制如何变瘦，越大瘦的越多，默认是1 flex-shrink:0是防止变瘦
flex-basis 基准宽度，默认是auto，忽略~
align-self 单独让某一个item的次轴对齐方式

## 底线
没设计稿我做个p
## 草图软件
* Figma
* 墨刀



