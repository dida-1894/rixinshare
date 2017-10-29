1.单列布局

水平居中
1.1.1

使用inline-block 和 text-align实现
.parent{text-align: center;}
.child{display: inline-block;}
优点：兼容性好；不足：需要同时设置子元素和父元素


.child{width:200px;margin:0 auto;}
优点：兼容性好缺点: 需要指定宽度

1.1.3使用table实现

1.1.4使用绝对定位实现


垂直居中
对于行内元素(inline)
单行：设置上下 pandding 相等；或者设置 line-height 和 height 相等
多行：设置上下 pandding 相等；或者设置 display: table-cell; 和 vertical-align: middle;；或者使用 flex 布局；或者使用伪元素
对于块级元素(block)：下面前两种方案，父元素需使用相对布局
已知高度：子元素使用绝对布局 top: 50%;，再用负的 margin-top 把子元素往上拉一半的高度
未知高度：子元素使用绝对布局 position: absolute; top: 50%; transform: translateY(-50%);

2.多列布局
双列 slide定宽 content自适应
三列： 
圣杯
总体上看上、中、下三个部分，一般写三组<div></div>标签
所谓布局都是在中间部分做文章，有几个要求：第一最中间部分宽度是不定的；第二：俩侧边栏宽度是定的
为达目的，我们肯定要采用浮动，但是有个诀窍：此处html结构中中间部分要先写，所以html结构是下面这样的
 <div id="header">header</div>
 <div id="main">
         <div class="content">三栏式圣杯布局</div>
         <div class="aside">定宽左侧边栏</div>
         <div class="extra">定宽右侧栏</div>
 </div>
 <div id="footer">footer</div>
当我们给一个div加上左负margin自然这个区块就向左位移了。思考一下就知道如果我们给俩边栏设置的都是 float:left属性，则需要左侧边栏向左位移一整个父容器的宽度，右侧边栏则向左位移一个自身宽度。

直接给父元素加个padding，俩侧边栏使用一个相对定位移到padding区域就搞定了。

 #main {
         padding: 0 200px;
     }

aside左移-200
extra右移-200

<div class="mid">
        <div class="content">三栏式双飞翼布局中间自适应</div>
</div>    

.mid {
    float: left;
    width: 100%;    
}

.mid .mid-content {
	margin-left:200px;
    margin-right:200px;
}




响应式布局
1）媒体查询
2）流动布局


流布局与固定宽度布局基本不同点就在于对网站尺寸的测量单位不同。固定宽度布局使用的是像素，但是流布局使用的是百分比，看到百分比，你应该想到，这将提供了很强的可塑性和流动性。换句话说，通过设置了百分比，你将不需要考虑设备尺寸或者屏幕宽度大小了，结论就是，你可以为每种情形找到一种可行的方案，因为你的设计尺寸将适应所有的设备尺寸。

流布局与媒体查询和优化样式技术的关系密切。单纯的基于百分比宽度是不足以在一个大屏幕中实现你设计。


@media screen and (min-width:800px){
  .class
  {
    background:#666;
  }
}
	
<link rel="stylesheet" media="screen and (max-width: 400px)" href="mini.css" />


<meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
device-width ，主要是为了让整个页面宽度与手机可视宽度相同，这样就可以简单相容于不同机型屏幕大小，如果这边width沒有设定的话，就会依照html/css给予的width当作预设值。
user-scalable，这个属性可以让使用者能否放大、缩小页面，如果页面不允许手机使用者缩放，就直接设定0或者no，反之要启动缩放功能，就设置1或者是yes。


Name				Value					Description
width				正整数或device-width		定义视口的宽度，单位为像素
height				正整数或device-height		定义视口的高度，单位为像素
initial-scale		[0.0-10.0]				定义初始缩放值
minimum-scale		[0.0-10.0]				定义缩小最小比例，它必须小于或等于maximum-scale设置
maximum-scale		[0.0-10.0]				定义放大最大比例，它必须大于或等于minimum-scale设置
user-scalable		yes/no					定义是否允许用户手动缩放页面，默认值yes