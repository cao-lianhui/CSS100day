# 1.首先是 Html 和 一些 Js 代码的实现，主要看注释就行

Html 代码:

```
<div class="frame">
	<div class="stage"></div>
</div>
```

Js 代码:

```
let stage = document.querySelector('.stage');
let strStar = '';
// 创建 300 个盒子，用作星星
for(let i = 0; i < 300; i++){
	strStar += '<div class="star star-'+(i+1)+'"></div>';
}
// 创建 6 个盒子，背景使用流星图
for(let i = 0; i < 6; i++){
	strStar += '<div class="shooting-star shooting-star-'+(i+1)+'"></div>';
}
// 把星星和流星添加到页面中
stage.innerHTML = strStar;
```

Css 代码：

# 2.先画正方形的白色盒子居中显示

```
.frame{
    position: absolute;
	top: 50%;
	left: 50%;
	width: 400px;
	height: 400px;
	margin-top: -200px;
	margin-left: -200px;
	border-radius: 2px;
	box-shadow: 1px 2px 10px 0px rgba(0,0,0,0.1);
	overflow: hidden;
	background: #fff;
	color: #fff;
}
```

# 3.白色盒子中间通过渐变画实现接近夜色的背景，如下图

![img](https://github.com/cao-lianhui/CSS100day/blob/master/stars-42/images/stars1.png)

```
.stage{
    position: absolute;
	width: 280px;
	height: 280px;
	top: 60px;
	left: 60px;
	background: #1d4253;
	background: -moz-linear-gradient(top, #1d4253 0%, #6bb5c4 100%);
	background: -webkit-linear-gradient(top, #1d4253 0%, #6bb5c4 100%);
	background: linear-gradient(top, #1d42553 0%, #6bb5c4 100%);
	border-radius: 50%;
	overflow: hidden;
}
```

# 4.实现星星样式和在星空上随机分布

```
.star{
    position: absolute;
	width: 1px;
	height: 1px;
	border-radius: 1px;
	background: #fff;
}
@test: 280;
// 用函数实现星星随机分布
.showStar (@index) when (@index < @numberOfStars){
    // less 里 css 类名拼接方式
	.star-@{index}{
	    // 随机生成 top 和 left 的值，实现星星随机分布
		// 注意这里需要用到 js 代码，采用 `` 字符的方式存放 js 代码
		// 且 less 版本必须要在 3 以下、必须要在 3 以下、3 以下
		@distance: `Math.round(Math.random() * 280)`;
	    top: ~"@{distance}px";
		left: ~"@{distance}px";
	}
	.showStar(@index+1);
}
// 函数调用
.showStar(1);
```

效果如下图:

![img](https://github.com/cao-lianhui/CSS100day/blob/master/stars-42/images/stars2.png)

# 5.把流星图加入页面中，并用函数实现高度随机分布

```
// 加入流星图
.shooting-star{
    position: absolute;
	top: 0;
	left: 0;
	width: 120px;
	height: 2px;
	background: url(./images/shooting-star.png) center center no-repeat;
	background-size: 100% 100%;
	transform: rotate(20deg);
}

// 用函数实现流星在星空中高度随机分布
.showShoot (@index) when (@index < @numberOfShootingStars){
    .shooting-star-@{index}{
	    // 高度随机分布在 30px - 130px 之间
	    top: ~"`Math.random()*100 - 30`px";
		
	}
	.showShoot(@index+1);
}
.showShoot(1);
```

效果如下图所示：(注：把类名 stage 的 border-radius 先注释可以比较清楚的看到流星分布)

![img](https://github.com/cao-lianhui/CSS100day/blob/master/stars-42/images/stars3.png)

然后隐藏流星，设置类名 shooting-star 的 left 值为 -120px，和类名 stage 的 border-radius 

的值为 50%，恢复到只有星星的夜空

# 6.接下来用 @keyframes 实现星星闪烁和流星划过夜景的动画

```
// 实现星星在夜空中闪烁的动画
@keyframes flickr{
    0%, 100%{
	    opacity: 1;
	}
	50%{
	    opacity: 0.2;
	}
}

// 流星划过星空的动画
@keyframes shooting-star{
    0%{
	    transform: translate3d(0,0,0) rotate(20deg);
	}
	10%, 100%{
	    transform: translate3d(451px, 164px, 0) rotate(20deg);
	}
}
```

这时需要在 .showStar 函数里为每个星星添加动画，只要添加 animation 就可以了。如下所示

```
// 每个星星随机产生的动画时间 动画名称 动画延迟时间 动画模式为无限动画 
animation: ~"`Math.round((Math.random()*20+20)/10)`s" flickr ~"`Math.round(Math.random()*20/-10)`s" infinite;
```

效果如下图所示

![img](https://github.com/cao-lianhui/CSS100day/blob/master/stars-42/images/stars.gif)

同样的在 .showShoot 函数里添加 animation，实现流星划过夜空的场景

```
animation: ~"`Math.round(Math.random()*5+20)`s" shooting-star ~"`Math.round(Math.random()*250)/10`s" infinite;
```

最后效果如下图所示

![img](https://github.com/cao-lianhui/CSS100day/blob/master/stars-42/images/shooting-star.gif)


# 接下来可以扩展下流星效果，把流星效果扩展成整个页面的，如下图所示

![img](https://github.com/cao-lianhui/CSS100day/blob/master/stars-42/images/shooting-star2.gif)

先改变类名 frame 和 stage 的样式，只要是改变高度和宽度，还有 left top 值，如下图

```
.frame{
    position: absolute;
	top: 0;
	left: 0;
	width: 100%;
	height: 100%;
	overflow: hidden;
	background: #fff;
	color: #fff;
}
.stage{
    position: absolute;
	width: 100%;
	height: 100%;
	top: 0;
	left: 0;
	background: #1d4253;
	background: -moz-linear-gradient(top, #1d4253 0%, #6bb5c4 100%);
	background: -webkit-linear-gradient(top, #1d4253 0%, #6bb5c4 100%);
	background: linear-gradient(top, #1d42553 0%, #6bb5c4 100%);
	overflow: hidden;
}
```

星星随机分布的 top 和 left 值需要改变，方便铺满页面，星星的数量也要增加

下面是改过后的 showStar 函数

```
// 用函数实现星星随机分布
.showStar (@index) when (@index < @numberOfStars){
    // less 里 css 类名拼接方式
	.star-@{index}{
	    // 随机生成 top 和 left 的值，实现星星随机分布
		// 注意这里需要用到 js 代码，采用 `` 字符的方式存放 js 代码
		// 且 less 版本必须要在 3 以下
		@distance: `Math.round(Math.random() * 2000)`;
	    top: ~"`Math.round(Math.random() * 600)`px";
		left: ~"@{distance}px";
		animation: ~"`Math.round((Math.random()*20+20)/10)`s" flickr ~"`Math.round(Math.random()*20/-10)`s" infinite;
	}
	.showStar(@index+1);
}
// 函数调用
.showStar(1);

// Js 代码里星星的数量由原来的 300 增加到 4000
// 创建 4000 个 div，用作星星
for(let i = 0; i < 4000; i++){
	strStar += '<div class="star star-'+(i+1)+'"></div>';
}
```

流星的数量和分布值也要改变，下面是改过后的 shootStar 函数

```
// 用函数实现流星在星空中高度随机分布
.showShoot (@index) when (@index < @numberOfShootingStars){
    .shooting-star-@{index}{
		animation: ~"`Math.round(Math.random()*5+40)`s" shooting-star ~"`Math.round(Math.random()*250)/10`s" infinite;
	}
	.showShoot(@index+1);
}
.showShoot(1);

// 注意这时流星的 left 值有 Js 随机生成，不在是改变 top 值，数量增加到 200
// Js代码

for(let i = 0; i < 200; i++){
	strStar += '<div class="shooting-star shooting-star-'+(i+1)+'"></div>';
}
var shootStar = document.querySelectorAll('.shooting-star');
for(let i = 0; i < shootStar.length; i++){
	shootStar[i].style.left = Math.random()* document.documentElement.clientWidth + 'px';
}
```

最后实现流星的动画稍微改下，改成划过夜空后渐渐消失，改变 opacity

如下所示:

```
@keyframes shooting-star{
    0%{
	    opacity: 1;
	    transform: translate3d(0,0,0) rotate(20deg);
	}
	10%, 100%{
	    opacity: 0;
	    transform: translate3d(951px, 264px, 0) rotate(20deg);
	}
}
```

大概的流程就是这些啦，有不懂的主要去看源码哦o(*￣▽￣*)ブ

# 下面是原网站效果

[原网站效果](https://100dayscss.com/?dayIndex=41)
