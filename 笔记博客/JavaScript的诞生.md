
## js的诞生
> 网景公司想开发一种嵌入网页的脚本语言来为了解决一些简单的网页互动（比如，检查"用户名"是否填写），只要求功能不太复杂，容易学习。当时由于JAVA比较火，网景公司也想蹭一波热度，于是在1995年，34岁的系统程序员Brendan Eich被网景公司录用，为了应付公司安排的任务，他只用10天就把Javascript设计出来了。


## js的历史
### 浏览器大战
1. 微软：1996年8月IE 3 发布，支持JScript，浏览器大战开始，并且，每家浏览器的脚本不一样
2. 网景：1996年11月，向ECMA提交语言标准，因为版权问题，JS语言标准不叫JavaScript，叫ECMAScript


### IE6盛行
1. 由于IE被微软捆绑进了windows，1998年网景公司被微软收购了，临死前并将浏览器开源（firefox），2001年发布IE6伴随着windows XP，2004年IE6市场份额全球占比80%，所以在当时IE非常火。但是IE6的bug又比较多，于是Firefox又准备重新打败IE
2. 2005年，IE7发布，但是还是没有IE6的份额多
3. 2006年，主流的浏览器还是IE和Firefox
4. 2010年，因为国内用户使用的盗版XP系统较多，自带IE6，所以当时IE6占据了中国的浏览器市场


### Chrome出世
1. 由于IE6的成功，觉得没有对手了，微软决定解散IE6团队，只留下少数人维护
2. 2004年，谷歌招了些firefox和解散的IE团队的人来开发浏览器
3. 2008年，chrome发布了，并且拿下了浏览器市场的1%份额
4. 2011年，chrome的市场份额超过了firefox
5. 2016年，chrome的全球份额达到了62%

>因为IE6不兼容W3C制定的标准，随着移动市场的兴起，中国的前端逐渐摆脱了对IE的噩梦。2016年淘宝天猫，宣布不再兼容IE6，7，同年底宣布不支持IE8。从此前端极速发展。


### ECMAScript标准
1. 1997年6月，第一版ECMAScript发布
2. 1999年12月，第三版发布（使用最广的版本）
3. 2009年12月，第五版发布
4. 2015年6月 第六版发布，现在新浏览器都支持这一版
5. 之后每发布一版，版本号以年份命名

### js的兴起
1. 2004年，谷歌发布了在线网页版的Gamil
2. 2005年，Jesse把谷歌的技术命名为ajax
3. 2006年，jQuery发布，是使用最长的一个js库
4. 2009年，Ryan基于V8创建了Node.js
5. 2010年，Isaac基于Node.js写出了npm，TJ同年也发布了Express.js


## js的十大设计缺陷
1. 不适合开发大型程序
> Javascript没有名称空间（namespace，很难模块化，没有如何将代码分布在多个文件的规范，允许同名函数的重复定义，后面的定义可以覆盖前面的定义，很不利于模块化加载
2. 常小的标准库
> Javascript提供的标准函数库非常小，只能完成一些基本操作，很多功能都不具备
3. null和undefined
> 两者容易混淆，但是含义又不一样
4. 全局变量难以控制
> Javascript的全局变量，在所有模块中都是可见的；任何一个函数内部都可以生成全局变量，这大大加剧了程序的复杂性
5. 自动插入行尾分号
> Javascript的所有语句，都必须以分号结尾。但是，如果你忘记加分号，解释器并不报错，而是为你自动加上分号。有时候，这会导致一些难以发现的错误。


6. 加号运算符
> +号作为运算符，有两个含义，可以表示数字与数字的和，也可以表示字符与字符的连接。如果一个操作项是字符，另一个操作项是数字，则数字自动转化为字符。这样的设计，不必要地加剧了运算的复杂性，完全可以另行设置一个字符连接的运算符。

7. NaN
> NaN是一种数字，表示超出了解释器的极限。它有一些很奇怪的特性：与其设计NaN，不如解释器直接报错，反而有利于简化程序。

8. 数组和对象的区分
> 由于Javascript的数组也属于对象（object），所以要区分一个对象到底是不是数组，相当麻烦。
9. == 和 ===
> ==用来判断两个值是否相等。当两个值类型不同时，会发生自动转换，得到的结果非常不符合直觉.因此，推荐任何时候都使用"==="（精确判断）比较符。

10. 基本类型的包装对象
> Javascript有三种基本数据类型：字符串、数字和布尔值。它们都有相应的建构函数，可以生成字符串对象、数字对象和布尔值对象。

