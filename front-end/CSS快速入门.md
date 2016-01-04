## CSS 快速入门

## 基本属性
* color
* background
	* background: white url(test.jpg) repeat-x;
* background-color
* background-image： url(/test.jpg);
* background-repeat:   no-repeat;
	* repeat-x
	* repeat-y
* background-position: top left;
  	* top
  	* left
  	* right
  	* bottom
  	* center
* 如果每一组分量中的两位数字相同可以使用简写
	* `#ccbb00==#cb0` 
* float
* vertical-align: top //对齐 top middle bottom

### 字体
* font
	* font: font-style font-variant font-weight font-size/line-height font-family

* font-variant
	* normal
	* small-caps 小型大写字母
	* inherit  父类继承
* font-size 大小
	* 
	``` css
		body{
			font-size: 14px;
		}
		h1 {
			font-size: 150%; //相对于父元素
		}
		h2 {
			font-size: 1.2em; //1.2倍
		}
	```

	* 关键字指定
		* xx-small
		* x-small
		* small
		* medium
		* large
		* x-large
		* xx-large
		
	> 一般每级字体差20%大小，body默认为16像素 
		h1 200%,h2 150%,h3 120%,h4 100%,h5 90,h6 60%

* font-style  
	* bold 
	* normal
	* bolder //效果不明显，很少使用
	* lighter //效果不明显，很少使用
	* 100-900 //100的倍数，不常使用
	* italic 倾斜
* font-weight 粗细
* text-decoration 文本装饰
	* underline 下划线
	* line-through 删除线
	* overline 上划线
	* none 去除格式	
* text-align  文本对齐方式
	* center
* letter-spacing 文字间距
* line-height 行间距
	* 1.6 em
	* 160%

* list-style 列表外观
	* list-style-type: disc //默认 
		* dircle //圆圈
		* square //方块
		* none
	* list-style-image: url();
	* list-style-position: outside

## 伪类
* nth-child
	* nth-child(odd)  //奇数
	* nth-child(even) //偶数
	* nth-child(2n+1) //计算
* first-child
* last-child
* 超链接

``` css
//未访问
a:link {

}

//已访问
a:visited{

}

//悬停
a:hover{

}

//焦点
a:focus{
}

//活跃
a:active{
}

```
### 伪元素
* `:first-letter` 首字母
* `:first-line ` 第一行

### 属性选择器
* `img[width]` 包含width属性的图像
* `img[height = "300"]` 高度为300的图像
* `image[alt ~=flowers"]` alt 属性包含flowers的图像

### 兄弟元素
* `h1+p{ ... }` //选择所有p前面有h1的兄弟段落的 

## 盒子模型
### 边框
* border 加边框
	* border: thin solid #111111 //width style color 顺序任意
* border-color
* border-width
	* thin 细
	* medium 中
	* thick 粗
	* 1px
* border-style
	* solid 普通
	* double 双线
	* groove 槽线
	* outset 凸线
	* dotted 虚线
	* inset 凹线
	* dashed 破折线
	* ridge 脊线
* border-radius:15px // 圆角
* border-top(bottom,left,right)
	* border-top-color
	* border-top-style
	* border-top-width
	* border-top-left-radius: 3em
* border-collapse: collapse; //去除间距,针对表格
* padding 内边距
	* padding: 0px 10px 20px 10px //top right bottom left
	* padding: 10px 20px //top=bottom right=left
	* padding-left: 10px
* margin 外边距
	* margin-left...


## 布局
* 上下放置的两个块元素，外边距会采用两个块中较大外边距的一个，外边距不会叠加

### 浮动
* float 
* clear: right 右边不允许有浮动内容
* position： 
	* static //默认静态定位
	* absolute //绝对定位 相对于父元素
	* fixed 
	* relative //相对定位 相对于整个页面
* z-index 处理z的值

### 表格
* display
	* table
	* table-cell

### @font-face 导入字体
### @import 导入其它css

### @media 导入媒体
	
``` css	
`@media screen and (min-device-width: 481px) and （orientation:landscape）`{
	#guarantee{
		margin-right: 250px
	}
	body{
		...
	}
}
```

* min-device-width 设备的大小
* min-width 浏览器大小