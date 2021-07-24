## 什么是表达式和语句
```javascript
var a = 1+ 2;

var b = add(1,2);
```
* 比如1+2就是表达式，它的值是3
* add(1,2)就是表达式，它的值是函数的返回值
* 但是var a = 1+2;这一句就是一个语句
* 表达式一般都会产生一个值
* 语句一般是一些操作，比如赋值，一般情况下不需要返回值

## 标识符规则
1. 标识符中可以包含有字母，数字，下划线，$ 
2. 不能以数字开头，用字母、下划线、$都可以
3. 不能是关键字(var const if else ...等等)
4. js底层保存标识符时实际上是用的Unicode编码，所以理论上讲，所有的UTF-8中含有的所有字符都可用

## 

## 注释
1. 一般重要的时候写注释，不要直接翻译代码
2. 踩坑的时候可以写注释，比如遇到什么bug

## 区块
由{}包裹起来的区域
```javascript
{
    let a = 1;
    let b = 2;****
}
```

## if else语句
```javascript
if(a ===1){
    console.log(111)
}else if(a ===2){
    console.log(222)
}else{
    console.log('最后的分支')
}

```
1. if(表达式){语句1}else{语句2}  
2. {}里面只有一句的时候可以省略  
3. 判断条件最好写 === 不要写==
4. 逗号表示这句话没完  console.log(2),console.log(3)

## switch(基本不用)
```javascript
switch (a){
    case "apple":
        console.log("苹果")
        break;
    case "banana":
        console.log("香蕉")
        break;
    default:
        console.log("都不是")
}
```
1. break一定不要忘了

## 问好冒号表达式 （三元表达式）
```javascript
function (a,b){
    return a>b?a:b
}
```
1. 条件true就返回a，否则返回b


## &&  ||
1. a && b 短路逻辑，a为false的时候就取a
2. && 有个特点，前面条件为true时，会去求后面的值
3.  a || b 短路逻辑，a为true就取a 

## while
```javascript
let i = 1
while (i < 10>){
    console.log(i)
}
```
1. while (true){}死循环
2. 初始化 判断 循环体 增长 一个不写就死循环

## for循环
```javascript
for (语句1;表达式2;语句3){
    循环体
}
```
1. break 跳出离他最近的循环
2. continue 跳出本次循环，进入下一次循环

## label
```javascript
foo:{
    console.log(11)
    break foo;
    console.log(222)
}
console.log(2)
```
label相当于是给语句写了一个标志符，一般用于循环语句跳出指定的循环