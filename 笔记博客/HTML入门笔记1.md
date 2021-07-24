# HTML入门笔记1

### HTML的历史
Tim Berners-Lee （蒂姆·伯纳斯·李）简称**李爵士**，他是万维网的发明者，南安普顿大学与麻省理工学院教授。在1990年左右发明了HTML。

### HTML入门
```html
<!DOCTYPE html>
<html lang="zh-CN">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body></body>
</html>

```
1.首先新建一个页面，第一行先声明文件的文档类型浏览器才能获取文档的类型，这里的代表HTML5
```html
<!DOCTYPE html>
```
2.html标签里的 lang="zh-CN"是表示当前文档显示的语言。
3.head标签里面包含了几个meta标签

这个是声明文件的字符编码，一般都用UTF-8
```html
<meta charset="UTF-8" />
```
这个是告诉IE使用edge内核
```html
<meta http-equiv="X-UA-Compatible" content="IE=edge" />
```
这个标签的作用是设置显示窗口width=device-width的意思是显示窗口宽度为设备的屏幕宽度，initial-scale=1.0是表示禁用缩放。
```html
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
```
这个标签里的文字就是浏览器tab上的文字
```html
<title>这是标题</title>
```
body标签就主要写页面的内容

### 常用的章节标签

* h1-h6 标题的标签，字体会从大到小
* section 章节标签
* article 文章标签
* p 段落标签
* header 头部标签
* footer 脚部标签
* main 主要内容标签
* aside 旁支内容
* div 划分一块区域

### 全局属性
所有标签都有的属性：class contenteditable hidden id style tabindex title

### 常用的内容标签
* ol+li 表示有序列表
* ul+li 表示无需列表
* dl+dt+dd 表示描述列表
* pre 标签中的文本通常会保留空格和换行符，主要用来输出源代码
* hr 表示一条分割线
* br 表示一个换行符，有换行的作用
* a 表示一个超链接，点击可以跳转到其它页面
* em 主要是强调文本字面上的内容
* strong 主要是语气的强调
* code 可以显示源代码的样子
* q 表示引用，比较短的
* blockquote 也表示引用，但是比较长


