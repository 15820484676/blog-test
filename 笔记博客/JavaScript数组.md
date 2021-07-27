## JS数组
* js的数组不是典型数组，典型的数组是什么呢？
  *  元素的数据类型相同
  *  使用连续的内存存储
  *  通过数字下标获取元素
* js的数组是这样
  * 元素的数据类型可以不同
  * 内存不一定是连续的(数组其实是一种对象)
  * 不同通过数字下标(是通过字符串下标)
  * key可以是任意的：
   ```javascript
   let arr = [1,2,3]
   arr['xxx'] = 4
   console.log(arr)//[1,2,3,xxx:4]
   ```

## 创建数组
```javascript
直接创建：

let arr = [1,2,3]
let arr1= new Array(1,2,3)//数组的元素为1，2，3
let arr2 = new Array(3)//数组元素个数为3个

转化创建:

let arr = '1,2,3'.split(',')
let arr = '123'.split('')
Array.from('123')//把不是数组的尝试编程数组,可以把对象编程数组，对象需要有类似的下标属性和length属性

伪数组：
let divList = document.querySelector('div')
如果一个数组的原型链中并没有数组的原型，那么他就是伪数组,它的原型中没有数组的共有属性

合并两个数组：
let arr1 = [1,2,3]
let arr2 = [3,4]
let newArr1 = arr1.concat(arr2)//把两个数组合并成一个新数组[1,2,3,3,4]

截取数组：
let arr3 = [1,2,3,4,5]
let newArr2 = arr3.slice(2)//从下标2开始截取数组[3,4,5]

let arr4 = arr3.slice(0)//用来复制一个数组
```
## 数组增删改查
### 删除
```javascript
let arr = [1,2,3]
delete arr['0']
console.log(arr)//[empty,2,3]
删除后数组的长度居然不变，稀疏数组

let arr1 = [1,2,3]
arr.length = 1
也可以删除..

let arr = [1,2,3,4]
arr.splice(2,1)//从下标为2的位置删除一个元素
console.log(arr) // [1,2,4]

let arr = [1,2,3,4]
arr.splice(2,1,8)//第三个参数，删除下标位置的元素并添加8

let arr = [1,2,3,4]
arr.splice(2,1,8,9,10)//删除下标位置的元素并添加8,9,10
console.log(arr)//[1,2,8,9,10,4]

let arr = [1,2,3]
arr.push(5)//把一个元素添加到数组末尾
console.log(arr)// [1,2,3,5]
arr.pop()//把一个元素从数组末尾删除，并返回删除的元素

arr.shift(4)//把一个元素添加到数组开头
console.log(arr)//[4,1,2,3]
arr.unshift()//把数组开头的一个元素删除

arr.join()//把数组内的元素连接成一个字符粗
console.log(arr.join('---'))//1---2---3
```

### 查看所有元素
* Object.keys(arr) //可以拿到数组的属性名
* for循环查看
```javascript
//自己控制key的增长
let arr = [1,2,3]
for (let i=0;i< arr.length;i++){
    console.log(arr[i])
}
```
* forEach
```javascript
let arr = [1,2,3]
arr.forEach(function (x,y){
    console.log(`key: ${y} value: ${x}`)
})
//原理是遍历数组，把数组每一项都传到函数里去
```
* forEach和for循环的区别：
  * for循环可以加break 和continue
  * forEach是一个函数，for循环是一个关键字，块
  
* 查看单个属性
  * arr[0]查看单个
  * arr[arr.length] === undefined //索引越界
  * arr[-1] === undefined //索引越界
```javascript
for(let i = 0;i<=arr.length;i++){
console.log(arr[i].toString())
}
//报错：Cannot read property 'toString' of undefined 意思是不能读取undefined的toString属性

let arr = [1,2,3,4]
arr.indexOf(3)//找到元素，如果是-1就是没有，有就返回第一个找到的下标
arr.find(function(x){
    return x%5 ===0
})
//返回满足函数条件的第一个元素

arr.reverse()//反转数组，会修改原来的数组
arr.sort()//数组排序
arr.sort(function (a,b){
    if (a>b){
        return -1
    }else if(a ===b){
        return 0
    }else{
        return 1
    }
})
//返回-1代表小，0代表等于，1代表大
```

### 数组变换 map filter reduce区别
map:n变成n
```javascript
//每一项的平方
let arr = [1,2,3,4]
let arr2 = arr.map(x => x*x)
console.log(arr2)//[1,4,9,16]
```
filter:n变少 返回true就是需要留下的，false就是剔除的
```javascript
//取出偶数
let arr = [1,2,3,4]
let arr1 = arr.filter(x=>x %2 ===0)
console.log(arr1)//[2,4]
```
reduce: n变1,最屌的一个 可以用它实现其它的方法
```javascript
//求和
let arr = [1,2,3,4]
arr.reduce((sum,item)=>{return sum+item},0)
//0其实就是初始值（可以是其它对象）,sum其实是retrun 后面的东西
```


