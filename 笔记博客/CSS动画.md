# CSS动画
由许多的画面组成（帧）
## 定时器
```html
var id = setInterval(()=?{
    console.log(111)
},1000)
```
每隔一段时间执行某个函数
## 性能
* 元素上ESC选择Paint flashing 可以看到元素是否在绘制

## 渲染过程


## 更新样式
* 用JS来更新样式div.style.background='red'，dib.classList.add('add')
* 最好加类 class
### 三种更新方式
* div.remove()会触发当前消失，其它元素relayout.准确的说是会重新布局，重新绘制，重新合成
* 只改变背景颜色 会触发绘制。合成
* transform 会触发合成
## 哪里查看哪种属性会触发什么？
CSS triggers  :csstriggers.com
## 动画优化
1.js优化：使用requestAnimationFrame代替setTiemout或setInterval  

2.CSS优化：使用will-change或translate
### transform介绍
* transform：translateX(100px)向x轴移动
* transform: translateY(100px) 向Y轴移动
* transform: translateX(100px) 向屏幕前移动，父容器要加perspective属性 
* transform: translate3d(x,y,z)，父容器要加perspective属性 
* transform:scale(1.5)放大多少 支持scaleX,scaleY
* transform :rotate(160deg)旋转多少度，一般用来做loading
* transform:skewY() 倾斜
* 多个属性可以组合
* 

## 元素居中
```html
demo{
    left:50%;
    top:50%;
    transform:translate(-50%,-50%)
}
```

## transition 过渡
* transition :all 1s 从快到慢  
* transition :all 1s linear 线性，匀速的
* transition:属性名 时长 过渡方式 延迟 
* 如果有多个动画可以使用setTimeout来实现
### 不是所有属性都能过渡
* display:none =>block,一般用visiblity:hidden=>visible
### display和visibility的区别

## 动画 animation
两种写法，百分号写的广泛点：  

  ```html
  @keyframes aaa {
        0% {
          transform: none;
        }
        50% {
          transform: translateX(200px);
        }
        100% {
          transform: translateY(200px, 200px);
        }
      }

    @keyframes bbb {
        from {
          transform: translateX(200px);
        }
        to {
          transform: translate(200px, 200px);
        }
      }
 ```
* animation:时长 过渡方式 延迟 次数 方向 填充模式 是否暂停 动画名 
* 时长：1s 
* 过渡方式：linear  ease ease-in ease-out ease-in-out
* 延迟：时间
* 次数：1 2 3  或者 infinite(无限循环)
* 方向：reverse alternate alternate=reverse 反方向 交替 。。
* 填充模式： none forwards backwards both  
* 是否暂停：paused running 动画暂停 运行 
