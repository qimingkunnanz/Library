# css:

## 一. 选择器

### 1). 基础选择器

- id选择器

- 类选择器

- 标签选择器

### 2). 复合选择器

- 后代选择器
  - p span
- 伪类选择器
  + a:link：链接被选中前的状态
  + a:visited：链接被访问后的状态
  + a:hover：链接被鼠标覆盖时的状态
  + a:active：链接被激活时的状态

## 二. 三大特性

### 1). 层叠

- 样式冲突,就近选择

### 2). 继承

- text-
- font-
- line-
- color

### 3). 优先级

- !important
- 行内样式
- id
- 类
- 标签
- 继承
- *

## 三.样式

### 1). font-文字属性
- font-size：字体大小
- font-family：字体类别(黑体,防宋)
- font-weight：字体粗细
 	- 加粗 700/bold
 	- 不加粗 400/normal
- font-style：字体样式
 	- 倾斜italic
 	- 不倾斜normal
- 复合属性
 	- font: font-style  font-weight  font-size/line-height  font-family;
 	- 至少要写字体大小和类别	font: 18px '微软雅黑';

 	- font: bold italic 18px/30px   ‘火星文’, '黑体','宋体',Arial

### 2). 文本样式
- color：文本颜色
- direction: 文本的方向(纵向/横向)
- line-height: 行高
- unicode-bidi: 设置文本方向
- text-align: 文本水平对齐方式
- text-indent: 首行缩进
	- 首行缩进两个字 text-indent: 2em;
- text-decoration: 文本的装饰
	- none  去掉线
	- underline  下划线
	- line-through  删除线  中划线
	- overline  上划线
- text-shadow: 文本阴影
- text-transform: 文本大小写
- text-overflow: 文本溢出包含元素时
    - clip 修剪文本
    - ellipsis 超出显示省略号
    - string 使用指定字符代替被修剪文本
- text-shadow: 文本添加阴影
### 3). 背景样式
- 简写 背景属性
    - background: 背景色 背景图 平铺 水平 垂直
    - background: linear-gradient(left, #FA5A55, #FA994D) 背景色渐变
- background-color: 背景颜色
    - rgb   颜色
    - rgba   透明度
- background-image: 背景图片
    - url
- background-position: 背景位置
    - top left right bottom center
    - x% y%
    - x y
- background-repeat: 背景显示方式
    - no-repeat   不平铺
    - repeat-x  横向平铺
    - repeat-y  纵向平铺
    - repeat   两个方向都平铺
- background-attachment: 背景是否固定
    - scroll 背景滚动
    - fixed 背景固定
- background-size: 背景图片尺寸
- background-origin: 背景图片根据定位区域
    - padding-box 内边距
    - border-box 边框盒
    - content-box 内容盒
### 4). 盒子模型
- 外边距：margin
    margin-top：上外边距
    margin-right：右外边距
    margin-bottom：下外边距
    margin-left：左外边距
    margin：top right bottom left；综合写法
    margin：0 auto；可让块级盒子水平居中
- 内边距：padding
    padding-top：上外边距
    padding-right：右外边距
    padding-bottom：下外边距
    padding-left：左外边距
    padding：top right bottom left；综合写法
    padding：0 auto；可让块级盒子水平居中
- 边框：border
    - border : border-width || border-style || border-color  
    - border-width：边框粗细
    - border-style：边框样式
        - none 无
        - solid 实线
        - dotted 点线
        - dashed 虚线(大多数浏览器为实现)
    - border-color：边框颜色
- 边框和内边距会撑大盒子，上下的盒子和嵌套的盒子注意上外边距塌陷问题
### 5). 动画
transition: all 1s 动画过渡效果(给自身加)

一般不会使用华丽的动画会使网页变卡

1.定义（keyframes：动画帧）
- @keyframes ani_div {
    0%{
        width: 100px;
        background-color: red;
    }
    50%{
        width: 150px;
        background-color: green;
    }
    100%{
        width: 300px;
        height: 300px;
        background-color: yellow;
        }
    }

2.调用
- div {
  width: 200px;
  height: 200px;
  background-color: aqua;
  margin: 100px auto;
  /* 2 调用动画 */
  animation-name: ani_div;
  /* 持续时间 */
  animation-duration: 2s;
}


/*行高可以撑宽盒子大小*/
/*浏览器设置文字大小从10px之后开始改变（0-9px大小一样）*/
/*添加浮动之后可以添加定位*/
/*只有hover才能被除a以外的元素使用*/
/* transparent : 透明色*/ 
/*背景图片是不会经常换的*/
/*使子盒子超出父盒子前提父盒子必须有宽*/
/*宽高不能被继承（内容撑开盒子）*/
/*并集选择器后执行*/
/*#空连接点击后回到页面顶部（刷新一次页面）*/
/*js空连接：可以点击但是不会刷新页面*/
/*a链接可以执行js代码*/
/*html5标签可以写任意属性*/