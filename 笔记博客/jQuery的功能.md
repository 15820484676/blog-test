## jQuery

jQuery是目前使用最广泛的js库。

## jQuery的功能

### 获取元素

* 使用jQuery需要先给jQuery构造函数传入一个选择表达式

* jQuery的别名是$符号，简短，比较方便

```javascript

$('#test')//这样就得到了一个jQuery对象

//表达式可以是css选择器

$(document) //选择整个文档对象

$('div.red') // 选择class为red的div元素

$('input[name=first]') // 选择name属性等于first的input元素

//表达式还可以是jQuery特有的表达式

$('a:first') //选择网页中第一个a元素

$('tr:odd') //选择表格的奇数行

$('#myForm:input') // 选择表单中的input元素

$('div:visible') //选择可见的div元素

$('div:gt(2)') // 选择所有的div元素，除了前三个

$('div:animated') // 选择当前处于动画状态的div元素

```

### 链式操作

* jQuery设计思想之一，就是最终选中网页元素以后，可以对它进行一系列操作，并且所有操作可以连接在一起，以链条的形式写出来

* 它的原理在于每一步的jQuery操作，返回的都是一个jQuery对象，所以不同操作可以连在一起。

```javascript

//find()操作返回的是find找到的jQuery对象，addClass操作返回的也是find找到jQuery对象

$('#test').find('.child').addClass('red').adClass('yellow')

$('#test')//选择id=test的元素

.find('.child')// 找到选择元素的class='child'的子元素

.addClass('red')//给找到的子元素添加class='red'

.addClass('yellow')//给找到的子元素添加class='yellow',多个添加是增量的方式

```

### 创建元素

* 创建元素，只要把新元素直接传入jQuery的构造函数就行了

```javascript

//创建一个div元素

let div = $('<div>这是一个jQuery创建出来的元素</div>')

div.text = '我改变了div的文本'

//append方法把创建的元素添加到其它元素的最后一个子节点

$('#test').append(div)

//prepend方法在元素开始的时候追加元素（第一个子节点）

$('#test').prepend(div)

//after方法在元素之后添加元素（添加弟弟节点）

$('#test').after(div)

//before方法在元素之前添加元素（添加哥哥节点）

$('#test').before(div)

```

### 移动元素

* jQuery设计思想之一，就是提供两组方法，来操作元素在网页中的位置移动。一组方法是直接移动该元素，另一组方法是移动其他元素，使得目标元素达到我们想要的位置。

```javascript

//.insertAfter()和.after()：把元素div移动到div2后面

$('div').insetAfter($('div2'))

$('div2').after($('div'))

//.insertBefore()和.before()：把元素div移动到div2前面

$('div').insertBefore($('div2'))

$('div2').before($('div'))

//.appendTo()和.append()：把元素div移动到div2里面，放到最后一个子节点

$('div').appendTo($('div2'))

$('div2').append($('div'))

//.prependTo()和.prepend()：把元素div移动到div2里面，放到第一个子节点

$('div').prependTo($('div2'))

$('div2').prepend($('div'))

```

### 改变元素的属性

* jQuery设计思想之一，就是使用同一个函数，来完成取值（getter）和赋值（setter），即"取值器"与"赋值器"合一。到底是取值还是赋值，由函数的参数决定。

* attr()方法用来设置或返回被选元素的属性值。

```javascript

//传入单个参数时,获取元素的属性

$('div').attr('width')

//传入两个参数时，设置元素的属性

$('div').attr('width','100px')

//传入一个对象时，设置元素的多个属性

$('div').attr({width:'100px',height:'100px'})

```