# CSS100day

本仓库的 ```css``` 动画都是在 [100daycss](https://100dayscss.com/) 网站上去练习，完成的。

仓库里用的 ```css``` ，都是 ```less``` 编译完成。

```Less``` 介绍：

```Less``` 是一门 ```CSS``` 预处理语言，它扩充了 ```CSS``` 语言，增加了诸如变量、混合（mixin）、函数等功能，让 ```CSS``` 更易维护、方便制作主题、扩充。

```Less``` 安装：npm i less -g

```Less``` 编译：lessc 文件名.less 文件名.css

```Less``` 的使用

1、```Less``` 声明变量：

```
@color: white;
h1{
   color: @color;
}
```

2、 ```Less``` 递归实现循环：
```
// @index 作为函数的形参
.Fun(@index) when ( @index <= 4 ){
    @top: @index * 2;
    .slice-@{top}{
        transform: translateY(40px);
    }
    @bottom: @top - 1;
    .slice-@{bottom}{
        transform: translateY(-40px);
    }
    // 递归调用函数
    .Fun(@index+1);
}
.Fun(1);

```

3、用 ```Less``` 实现继承：
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

大概先这些，后续接触了会持续更新哦，文件里哪里有更好改进的欢迎 push (*￣︶￣)
