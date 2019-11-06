# day03-CSS3【控制样式，网页布局】

## CSS3中新特性样式篇

### 背景

```css
background-origin：   规定背景图片的定位区域。
	☞ padding-box    背景图像相对内边距定位（默认值）
	☞ border-box	 背景图像相对边框定位【以边框左上角为参照进行位置设置】
	☞ content-box    背景图像相对内容区域定位【以内容区域左上角为参照进行位置设置】

   备注：
		1. 默认盒子的背景图片是在盒子的内边距左上角对齐设置。


background-clip：  	 规定背景的绘制区域。
	☞ border-box	 背景被裁切到边框盒子位置 【将背景图片在整个容器中显示】
	☞ padding-box	 背景被裁切到内边距区域【将背景图片在内边距区域（包含内容区域）显示】
	☞ content-box	 背景被裁切到内容区域【将背景图片在内容区域显示】


background-size：     规定背景图片的尺寸。
	☞ cover
	☞ contain
```

### 边框

```css
 box-shadow：      盒子阴影
 border-radius：   边框圆角
 border-image:	  边框图片

	 
			 /* 设置边框图片 */
			 border-image-source: url("2.png");

			 /* 边框图片裁切 : 不需要带单位*/
			 border-image-slice: 20;

			 /* 设置边框图片的平铺方式 */
			 /* border-image-repeat: stretch; */
			 border-image-repeat: round;
			/*  border-image-repeat: repeat; */

			border-image-width: 20px;
```

### 文本

```css
  ☞text-shadow： 设置文本阴影		
```

## CSS3新特性之选择器篇

```css
☞ 属性选择器： 
		[属性名=值] {}
		[属性名] {}	   匹配对应的属性即可
		[属性名^=值] {}    以值开头
		[属性名*=值] {}    包含
		[属性名$=值] {}	   以值结束
	
☞ 结构伪类选择器：
	  :first-child {}     选中父元素中第一个子元素
	  :last-child {}	  选中父元素中最后一个子元素
	  :nth-child(n) {}    选中父元素中正数第n个子元素
	  :nth-last-child(n) {}    选中父元素中倒数第n个子元素

	  备注；
		 n 的取值大于等于0
	     n 可以设置预定义的值
			odd[选中奇数位置的元素]  
			even【选中偶数位置的元素】

	     n 可以是一个表达式：
			 an+b的格式

☞ 其他选择器：
	:target          被锚链接指向的时候会触发该选择器
	::selection	     当被鼠标选中的时候的样式
	::first-line	 选中第一行
	::first-letter	 选中第一个字符
```

## CSS3新特性之颜色渐变

```CSS
  ☞ 线性渐变：
		 1. 开始颜色和结束颜色
		 2. 渐变的方向
	     3. 渐变的范围

	   background-image:  linear-gradient(
                to right,
                red,
                blue
		);

	备注：
	 	表示方向：
			 1. to + right | top | bottom | left 
			 2. 通过角度表示一个方向
			   0deg [从下向上渐变] 
			   90deg【从左向右】
  
  ☞ 径向渐变：
		   /* 径向渐变 */
			background-image: radial-gradient(
				 100px at center,
				 red,
				 blue
			);
```

## 2D转换

```css
  ☞ 位移
	   transform: translate(100px,100px);
		
	   备注：
	 	   位移是相对元素自身的位置发生位置改变

  ☞ 旋转
		transform: rotate(60deg);
	   备注：
		   取值为角度
  ☞ 缩放
	    transform: scale(0.5,1);
		备注：
			 取值为倍数关系，缩小大于0小于1，放大设置大于1
	
  ☞ 倾斜
	   transform: skew(30deg,30deg);
   	   备注：
		  第一个值代表沿着x轴方向倾斜
		  第二个值代表沿着y轴方向倾斜
```

## 3D转换

```css
  ☞ 位移
	transform: translateX()  translateY()   translateZ()

  ☞ 旋转
	 transform: rotateX(60deg)  rotateY(60deg)  rotateZ(60deg);

  ☞ 缩放
	  transform: scaleX(0.5)  scaleY(1)  scaleZ(1);
  ☞ 倾斜
      transform: skewX(30deg) skewY();

  ☞ transform-style: preserve-3d;
	 将平面图形转换为立体图形
```


## CSS3新特性之动画篇

### 过渡

```css
 https://www.cnblogs.com/afighter/p/5731293.html

 补间动画

			/* 设置哪些属性要参与到过渡动画效果中： all */
			transition-property: all;

			/* 设置过渡执行时间 */
			
			transition-duration: 1s;

			/* 设置过渡延时执行时间 */
			transition-delay: 1s;

			/* 设置过渡的速度类型 */

			transition-timing-function: linear;
```

### 动画

```css
  
	/* 1定义动画集 */
		@keyframes  rotate {

			/* 定义开始状态  0%*/
			from {
				transform: rotateZ(0deg);
			}

			/* 结束状态 100%*/
			to {
			   transform: rotateZ(360deg);
			}
		}



    注意：
		 1. 如果设置动画集使用的是百分比，那么记住百分比是相对整个动画执行时间的。
```


## CSS3新特性之网页布局篇

### 伸缩布局或者弹性布局【响应式布局】

```css
  ☞ 设置父元素为伸缩盒子【直接父元素】
	    display： flex
	
      为什么在伸缩盒子中，子元素会在一行上显示？
			 1. 子元素是按照伸缩盒子中主轴方向显示
			 2. 只有伸缩盒子才有主轴和侧轴
			 3. 主轴： 默认水平从左向右显示
			 4。 侧轴： 始终要垂直于主轴

  ☞ 设置伸缩盒子主轴方向（flex-direction）
		   	flex-direction: row; 【默认值】
			flex-direction: row-reverse;
			flex-direction: column;
			flex-direction: column-reverse;
  ☞ 设置元素在主轴的对齐方式( justify-content)
		/* 设置子元素在主轴方向的对齐方式 */
			justify-content: flex-start;
			justify-content: flex-end;
			justify-content: center;
			justify-content: space-between;
			justify-content: space-around;

  ☞ 设置元素在侧轴的对齐方式 （align-items）
			align-items: flex-start;
			align-items: flex-end;
			align-items: center;

			/* 默认值 */
			align-items: stretch;

  ☞ 设置元素是否换行显示（flex-wrap）
		  1. 在伸缩盒子中所有的元素默认都会在一行上显示
		  2. 如果希望换行：
			flex-wrap: wrap | nowrap;

  ☞ 设置元素换行后的对齐方式（ align-content）
		    align-content: flex-start;
			align-content: flex-end;
			align-content: center;
			align-content: space-around;
			align-content: space-between;
			/* 换行后的默认值 */
			align-content: stretch;
```



