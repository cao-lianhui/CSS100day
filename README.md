# CSS100day

本仓库的 CSS 动画是在 [100daycss](https://100dayscss.com/) 网站上去练习，完成的。

仓库里用的 CSS 用 Less 编译完成。

Less 介绍：Less 是一门 CSS 预处理语言，它扩充了 CSS 语言，增加了诸如变量、混合（mixin）、函数等功能，让 CSS 更易维护、方便制作主题、扩充。

Less 安装：npm i less -g

Less 编译：lessc 文件名.less 文件名.css 如：lessc index.less index.css

Less 的使用（下面的例子仅供参考）

#### 1、Less 声明变量：

```
@color: white;
h1{
   color: @color;
}
```

#### 2、Less 函数声明：

```
@fontSize: 24;
.Func(){
   color: red;
   // 字符串拼接
   font-size: @fontSize * 1px;
}
h1{
   // 调用函数， 导入样式
   .Func();
}
// 编译后
h1{
   color: red;
   font-size: 24px;
}
```

#### 2、 Less 递归实现循环：
```
// @index 作为函数的形参
.Func(@index) when (@index <= 8){
  @nullBase: @index - 1;
  .slice-@{index}{
      background-position: @nullBase * -50px 0;
      // transform: translateY(-40px);
      opacity: 1;
  }
  // 递归调用
  .Func(@index+1);
}
// 函数调用
.Func(1);

```

#### 3、用 Less 实现样式继承：
```
h1{
   color: white;
   height: 100px;
}
h2{
   &:extend(h1);  // 实现 h2 继承 h1 的样式
   width: 200px;
}
```
#### 4、Less 字符串，类名，单位拼接方式：
```
css类名拼接：
.class@{变量名}

字符串拼接：
1）~'@{变量名}字符串' 或 ~'字符串@{变量名}'
如：~'@{index}dads'
2）e('@{变量名}字符串') 或 e('字符串@{变量名}')
如：e('dads@{index}')
像素 px 或时间秒 s 之类的单位拼接
width: @{变量名} + 50px;
transition: @{变量名} + 2s;

当直接用变量名表示整个单位时的拼接方式：
width: @{index} * 1px; 或 width: @{index} + 0px;
表示其他单位也类似。
而不能用下面这种方式
width: (@变量名 + 50) + px;
这样的编译结果是：
width: 50 px
单位和数字之间会出现空格，width无法生效。

还有就是这几种拼接方式不能相互替换，否则会报错：ParseError: Unrecognised input in....
```
大概先这些，后续接触了会持续更新哦，对文件中代码有更好建议的欢迎 fork (*￣︶￣)
