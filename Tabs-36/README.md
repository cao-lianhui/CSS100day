### 1.首先是 Html 代码的实现

```
<div class="frame">
	<div class="center">
		<div class="tabs">
		    <!-- 顶部导航栏背景 -->
			<div class="top"></div>
			
			<!-- 四个 tab 切换按钮 -->
			<input type="radio" id="tab-1" name="rd" checked="checked"/>
			<label class="tab" for="tab-1">
				<span class="fa"></span>
			</label>
			
			<input type="radio" id="tab-2" name="rd" />
			<label class="tab" for="tab-2">
				<span class="fa"></span>
			</label>
			
			<input type="radio" id="tab-3" name="rd" />
			<label class="tab" for="tab-3">
				<span class="fa"></span>
			</label>
			
			<input type="radio" id="tab-4" name="rd" />
			<label class="tab" for="tab-4">
				<span class="fa"></span>
			</label>
			
			<label class="tab search">
				<span class="fa"></span>
			</label>
			
			<!-- tab 对应的内容区域 -->
			<div class="content">
				<div class="box" id="box-1">
					<h1>Dashboard</h1>
					<p>
						<span style="width: 250px;"></span>
						<span style="width: 270px;"></span>
						<span style="width: 235px;"></span>
						<span style="width: 260px;"></span>
						<span style="width: 53px;"></span>
					</p>
					<p>
						<span style="width: 262px;"></span>
						<span style="width: 234px;"></span>
						<span style="width: 246px;"></span>
						<span style="width: 260px;"></span>
						<span style="width: 144px;"></span>
					</p>
				</div>
				<div class="box" id="box-2">
					<h1>Comments</h1>
					<p>
						<span style="width: 250px;"></span>
						<span style="width: 270px;"></span>
						<span style="width: 235px;"></span>
						<span style="width: 260px;"></span>
						<span style="width: 53px;"></span>
					</p>
					<p>
						<span style="width: 262px;"></span>
						<span style="width: 234px;"></span>
						<span style="width: 246px;"></span>
						<span style="width: 260px;"></span>
						<span style="width: 144px;"></span>
					</p>
				</div>
				<div class="box" id="box-3">
					<h1>Notification</h1>
					<p>
						<span style="width: 250px;"></span>
						<span style="width: 270px;"></span>
						<span style="width: 235px;"></span>
						<span style="width: 260px;"></span>
						<span style="width: 53px;"></span>
					</p>
					<p>
						<span style="width: 262px;"></span>
						<span style="width: 234px;"></span>
						<span style="width: 246px;"></span>
						<span style="width: 260px;"></span>
						<span style="width: 144px;"></span>
					</p>
				</div>
				<div class="box" id="box-4">
					<h1>Setting</h1>
					<p>
						<span style="width: 250px;"></span>
						<span style="width: 270px;"></span>
						<span style="width: 235px;"></span>
						<span style="width: 260px;"></span>
						<span style="width: 53px;"></span>
					</p>
					<p>
						<span style="width: 262px;"></span>
						<span style="width: 234px;"></span>
						<span style="width: 246px;"></span>
						<span style="width: 260px;"></span>
						<span style="width: 144px;"></span>
					</p>
				</div>
			</div>
		</div>
	</div>
</div>
```

### 2.然后把盒子居中显示，和画出顶部导航，如下图所示

![img](https://github.com/cao-lianhui/CSS100day/blob/master/Tabs-36/images/tabs1.png)

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
	box-shadow: 1px 2px 10px 0px rgba(0,0,0,0.3);
	overflow: hidden;
	background-color: #2b3642;
	.center{
		position: absolute;
		width: 320px;
		height: 240px;
		top: 80px;
		left: 40px;
		background-color: #fff;
		box-shadow: 4px 8px 12px 0 rgba(0,0,0,0.3);
		.top{
			position: absolute;
			z-index: 1;
			top: 0;
			left: 0;
			right: 0;
			height: 40px;
			background-color: #3d4d5e;
		}
	}
}
```

### 3.画出每个 tabs 点击的样式，如下图所示


![img](https://github.com/cao-lianhui/CSS100day/blob/master/Tabs-36/images/tabs2.png)

```
.tab{
	position: relative;
	float: left;
	z-index: 5;
	width: 40px;
	height: 40px;
	text-align: center;
	line-height: 38px;
	color: #8398ad;
	cursor: pointer;
	font-size: 14px;
	transition: background .5s ease-in-out;
	.fa{
		position: absolute;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		margin: auto;
		width: 6px;
		height: 10px;
		border: 1px solid rgba(255, 255, 255, 0.4);
	}
	&.search{
		float: right;
	}
	&:hover{
		color: #fff;
	}
	&:hover .fa{
		border: 1px solid white;
	}
}
input[type="radio"]:checked + .tab{
	background: #5da2ed;
	color: #fff;
	.fa{
		border: 1px solid white;
	}
}
```

### 4.然后添加选项卡需要切换的每个内容， 如下图所示

![img](https://github.com/cao-lianhui/CSS100day/blob/master/Tabs-36/images/tabs3.png)

```
.star{
    position: absolute;
	width: 1px;
	height: 1px;
	border-radius: 1px;
	background: #fff;
}
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

### 5.把流星图加入页面中，并用函数实现高度随机分布

```
.content{
	position: absolute;
	top: 40px;
	color: #000;
	.box{
		position: absolute;
		top: 0;
		left: 0;
		opacity: 0;
		transform: translateY(3px);
		pointer-events: none;
		padding: 25px;
		transition: all .3s ease-in;
		h1{
			font-weight: 400;
			font-size: 16px;
			color: #415868;
			margin: 0;
			padding: 0;
		}
		p{
			margin: 17px 0;
			span{
				display: block;
				height: 4px;
				background: #e9e9e9;
				margin: 6px 0;
			}
		}
	}
}
```

上面图片中的内容会重叠在一起，因为没有设置属性 opacity 为 0，设置后内容就都变透明了

接下来开始下一个要切换的步骤

### 6.实现选项卡切换的效果

```
// 先默认实现显示第一个内容
#tab-1:checked ~ .content #box-1{
     pointer-events: all;
	 opacity: 1;
	 transform: translateY(0);
	 transition: all .5s ease-out .4s;
}

// 然后和上面相同，依次设置 4 个切换事件
#tab-1:checked ~ .content #box-1,
#tab-2:checked ~ .content #box-2,
#tab-3:checked ~ .content #box-3,
#tab-4:checked ~ .content #box-4{
     pointer-events: all;
	 opacity: 1;
	 transform: translateY(0);
	 transition: all .5s ease-out .4s;
}
```

最后效果图如下

![img](https://github.com/cao-lianhui/CSS100day/blob/master/stars-42/images/GIF.gif)


### 下面是原网站效果

[原网站效果](https://100dayscss.com/?dayIndex=35)
