7/4/2019 12:35:08 AM # 前端工具 

聚名网前端工具，小组成员上传或者更新时做好commit

---

## 目录
- [插件](#plugins)
  - [功能插件](#features)
     - [弹出层](#features)
     - [上拉加载，下拉刷新](#features)
     - [上传](#features)
     - [轮播图](#features)
     - [表单验证](#features)
     - [日期控件](#features)
     - [图表类插件](#features)
     - [拖拽类插件](#features)
     - [省市联动](#features)
     - [3D库](#features)
     - [HTML生成图片](#features)
     - [懒加载](#features)
  - [图片类插件](#images)
  - [移动端插件](#mobile)
  - [其他类插件](#other)
- [精选阅读](#read)
  - [前端技术](#fedev)
  - [Node 学习资料](#node_read)
  - [其他技术](#otherdev)


## 功能插件

### 弹出层

### [layer](http://layer.layui.com/?alone) - 适用于PC端

> **快速入门**
```javascript
//获得 layer 文件包后，解压并将 layer 整个文件夹（不要拆分结构） 存放到你项目的任意目录，使用时，只需引入 layer.js 即可。 
<script src="jQuery的路径"></script> <!-- 你必须先引入jQuery1.8或以上版本 -->
<script src="layer.js的路径"></script>

//弹出一个提示层
$('#test1').on('click', function(){
    layer.msg('hello');
}); 

//弹出一个页面层
$('#test2').on('click', function(){
   layer.open({
     type: 1,
     area: ['600px', '360px'],
     shadeClose: true, //点击遮罩关闭
     content: '\<\div style="padding:20px;">自定义内容\<\/div>'
   });
});

//弹出一个iframe层
$('#parentIframe').on('click', function(){
   layer.open({
     type: 2,
     title: 'iframe父子操作',
     maxmin: true,
     shadeClose: true, //点击遮罩关闭层
     area : ['800px' , '520px'],
     content: 'test/iframe.html'
   });
});

//弹出一个loading层
$('#test4').on('click', function(){
   var ii = layer.load();
   //此处用setTimeout演示ajax的回调
   setTimeout(function(){
     layer.close(ii);
   }, 1000);
});

//弹出一个tips层
$('#test5').on('click', function(){
   layer.tips('Hello tips!', '#test5');
});
```
> 想了解更多，可以取[官方文档](http://layer.layui.com/)找到

### [Layer For Mobile](http://layer.layui.com/mobile/) - 适用于移动端

> **快速入门**
```javascript
<script src="layer-mobile.js的路径"></script> <!-- 此库不依赖第三方库，移动版和PC版不能同时存在同一页面 -->

//信息框
layer.open({
   content: '移动版和PC版不能同时存在同一页面'
   ,btn: '我知道了'
});

//提示
layer.open({
   content: 'hello layer'
   ,skin: 'msg'
   ,time: 2 //2秒后自动关闭
});

//询问框
layer.open({
   content: '您确定要刷新一下本页面吗？'
   ,btn: ['刷新', '不要']
   ,yes: function(index){
     location.reload();
     layer.close(index);
   }
});

//底部对话框
layer.open({
   content: '这是一个底部弹出的询问提示'
   ,btn: ['删除', '取消']
   ,skin: 'footer'
   ,yes: function(index){
     layer.open({content: '执行删除操作'})
   }
});

//底部提示
layer.open({
   content: '一个没有任何按钮的底部提示'
   ,skin: 'footer'
});

//自定义标题风格
layer.open({
   title: [
     '我是标题',
     'background-color: #FF4351; color:#fff;'
   ]
   ,content: '标题风格任你定义。'
});

//页面层
layer.open({
   type: 1
   ,content: '可传入任何内容，支持html。一般用于手机页面中'
   ,anim: 'up'
   ,style: 'position:fixed; bottom:0; left:0; width: 100%; height: 200px; padding:10px 0; border:none;'
});

//loading层
layer.open({type: 2});

//loading带文字
layer.open({
   type: 2
   ,content: '加载中'
});
```
> 想了解更多，可以取[官方文档](http://layer.layui.com/mobile/api.html)找到

### 上拉加载，下拉刷新

### [Mescroll](http://www.mescroll.com/) - 精致的下拉刷新和上拉加载js框架，原生js，不依赖jquery，zepto，支持vue，一套代码多端运行

> **快速入门**
```javascript
//1. 下载并引用 mescroll.min.css , mescroll.min.js
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/mescroll.js@1.4.1/mescroll.min.css">
<script src="https://cdn.jsdelivr.net/npm/mescroll.js@1.4.1/mescroll.min.js" charset="utf-8"></script>
//2. 拷贝以下布局结构 :
<div id="mescroll" class="mescroll"> //id可以改,而"mescroll"的class不能删
	<div> //这个div不能删,否则上拉加载的布局会错位.(可以改成ul或者其他容器标签)
   	 //内容...
	</div>
</div>
//3. 固定mescroll的div高度. 推荐通过定位的方式,简单快捷:
.mescroll{
	position: fixed;
	top: 44px;
	bottom: 0;
	height: auto; /*如设置bottom:50px,则需height:auto才能生效*/
}
//4. 创建mescroll对象 :
var mescroll = new MeScroll("mescroll", { //第一个参数"mescroll"对应上面布局结构div的id (1.3.5版本支持传入dom对象)
	//如果您的下拉刷新是重置列表数据,那么down完全可以不用配置,具体用法参考第一个基础案例
	//解析: down.callback默认调用mescroll.resetUpScroll(),而resetUpScroll会将page.num=1,再触发up.callback
	down: {
		callback: downCallback //下拉刷新的回调,别写成downCallback(),多了括号就自动执行方法了
	},
	up: {
		callback: upCallback, //上拉加载的回调
		//以下是一些常用的配置,当然不写也可以的.
		page: {
			num: 0, //当前页 默认0,回调之前会加1; 即callback(page)会从1开始
			size: 10 //每页数据条数,默认10
		},
		htmlNodata: '<p class="upwarp-nodata">-- END --</p>',
		noMoreSize: 5, //如果列表已无数据,可设置列表的总数量要大于5才显示无更多数据;
				避免列表数据过少(比如只有一条数据),显示无更多数据会不好看
				这就是为什么无更多数据有时候不显示的原因.
		toTop: {
			//回到顶部按钮
			src: "../img/mescroll-totop.png", //图片路径,默认null,支持网络图
			offset: 1000 //列表滚动1000px才显示回到顶部按钮	
		},
		empty: {
			//列表第一页无任何数据时,显示的空提示布局; 需配置warpId才显示
			warpId:	"xxid", //父布局的id (1.3.5版本支持传入dom元素)
			icon: "../img/mescroll-empty.png", //图标,默认null,支持网络图
			tip: "暂无相关数据~" //提示
		},
		lazyLoad: {
    			use: true // 是否开启懒加载,默认false
    			attr: 'imgurl' // 标签中网络图的属性名 : <img imgurl='网络图  src='占位图''/>
    		}
	}
});
//5. 处理回调 :
//下拉刷新的回调
function downCallback() {
	$.ajax({
		url: 'xxxxxx',
		success: function(data) {
			//联网成功的回调,隐藏下拉刷新的状态;
			mescroll.endSuccess(); //无参. 注意结束下拉刷新是无参的
			//设置数据
			//setXxxx(data);//自行实现 TODO
		},
		error: function(data) {
			//联网失败的回调,隐藏下拉刷新的状态
			mescroll.endErr();
		}
	});
}

//上拉加载的回调 page = {num:1, size:10}; num:当前页 默认从1开始, size:每页数据条数,默认10
function upCallback(page) {
	var pageNum = page.num; // 页码, 默认从1开始 如何修改从0开始 ?
	var pageSize = page.size; // 页长, 默认每页10条
	$.ajax({
		url: 'xxxxxx?num=' + pageNum + "&size=" + pageSize,
		success: function(data) {
			var curPageData = data.xxx; // 接口返回的当前页数据列表
			var totalPage = data.xxx; // 接口返回的总页数 (比如列表有26个数据,每页10条,共3页; 则totalPage值为3)
			var totalSize = data.xxx; // 接口返回的总数据量(比如列表有26个数据,每页10条,共3页; 则totalSize值为26)
			var hasNext = data.xxx; // 接口返回的是否有下一页 (true/false)
			
			//联网成功的回调,隐藏下拉刷新和上拉加载的状态;
			//mescroll会根据传的参数,自动判断列表如果无任何数据,则提示空,显示empty配置的内容;
			//列表如果无下一页数据,则提示无更多数据,(注意noMoreSize的配置)
			
			//方法一(推荐): 后台接口有返回列表的总页数 totalPage
			//必传参数(当前页的数据个数, 总页数)
			//mescroll.endByPage(curPageData.length, totalPage);
					
			//方法二(推荐): 后台接口有返回列表的总数据量 totalSize
			//必传参数(当前页的数据个数, 总数据量)
			//mescroll.endBySize(curPageData.length, totalSize);
					
			//方法三(推荐): 您有其他方式知道是否有下一页 hasNext
			//必传参数(当前页的数据个数, 是否有下一页true/false)
			//mescroll.endSuccess(curPageData.length, hasNext);
					
			//方法四 (不推荐),会存在一个小问题:比如列表共有20条数据,每页加载10条,共2页.
			//如果只根据当前页的数据个数判断,则需翻到第三页才会知道无更多数据
			//如果传了hasNext,则翻到第二页即可显示无更多数据.
			//mescroll.endSuccess(curPageData.length);
			
			//结束下拉刷新的 mescroll.endSuccess()无参.
			//结束上拉加载 curPageData.length必传的原因:
				1.使配置的noMoreSize 和 empty生效
				2.判断是否有下一页的首要依据: 当传的值小于page.size时,则一定会认为无更多数据.
				  比传入的totalPage, totalSize, hasNext具有更高的判断优先级
				3.当传的值等于page.size时,才会取totalPage, totalSize, hasNext判断是否有下一页
				  传totalPage, totalSize, hasNext主要目的是避免方法四描述的小问题
			
			//设置列表数据
			//setListData(curPageData);//自行实现 TODO
		},
		error: function(e) {
			//联网失败的回调,隐藏下拉刷新和上拉加载的状态
			mescroll.endErr();
		}
	});
}		  
```
> 想了解更多，可以取[官方文档](http://www.mescroll.com/api.html?v=190725)找到






<h6 id="features">上传</h6>

- [jQuery File Upload](http://www.jq22.com/jquery-info230) - jQuery File Upload 是一个Jquery图片上传组件，支持多文件上传、取消、删除，上传前缩略图预览、列表显示图片大小，支持上传进度条显示；支持各种动态语言开发的服务器端。
- [imgUp](http://www.jq22.com/jquery-info13194) - jQuery多图上传插件imgUp.js
<h6 id="features">轮播图</h6>

- [Swiper](http://www.swiper.com.cn) - 强大的 Slider 库 其实这类效果库非常多，但文档能那么专业的就很少鸟
<h6 id="features">表单验证</h6>

- [Verify](http://www.jq22.com/jquery-info6134) - 一套完整的用户注册前端校验，包含用户名，密码强度，显示隐藏密码，手机号输入控制手机验证码，真实姓名，身份证号等验证。
<h6 id="features">日期控件</h6>

- [daterangepicker](http://www.daterangepicker.com) - 时间选择插件的不二选择，基于 ```Bootstrap``` 和 [Moment.js](http://momentjs.com/)
- [jedate](http://www.jemui.com/uidoc/jedate.html) - 是一款原生JS开发的 不依赖任何第三方库 大众化的日期控件
<h6 id="features">图表类插件</h6>

- [ECharts](http://echarts.baidu.com/index.html) - 好用，最关键的是支持的图表展示非常之多，强烈推荐
- [excellentexport](https://github.com/jmaister/excellentexport) - 纯前端的 Excel 导出，非常之方便
<h6 id="features">拖拽类插件</h6>

- [Sortable](https://github.com/RubaXa/Sortable) - 拖拽神器，用了就知道
<h6 id="features">省市联动</h6>

- [jquery.cityselect](https://github.com/akveo/blur-admin) - jQuery+JSON的省市三级、二级联动插件制订此文档。
<h6 id="features">3D库</h6>

- [three.js](https://github.com/mrdoob/three.js) - JavaScript 3D 库。超多的 [examples](http://threejs.org/examples/) 等着你去发现，你只需要关注内存和风扇就行了
<h6 id="features">HTML生成图片</h6>

- [html2canvas](https://github.com/niklasvh/html2canvas)+[canvas2Image](https://github.com/randreucetti/canvas2image) - 看这两库的名称就明白是做什么的。使用场景就是“动态生成的HTML可以长按保存为图片”。
<h6 id="features">懒加载</h6>

- [jquery.lazyload](http://www.jq22.com/yanshi390) - jQuery图片延迟加载插件jQuery.lazyload,使用延迟加载在可提高网页下载速度。在某些情况下，它也能帮助减轻服务器负载。

<h5 id="images">图片类插件</h5>

- [PhotoSwipe](http://photoswipe.com/) - 偶常用的 js 库 官网上有这么一句很关键、重要"no dependencies"
> ___```Swiper/PhotoSwipe/fullPage``` 有这仨库，微信里常见的 H5 页完全不是问题哒___
<h5 id="mobile">移动端插件</h5>

- [adaptive.js](https://github.com/Vibing/adaptive) - 借鉴手淘方案，adaptive.js将整个页面宽度平均分成10份，以clineWidth / 10的结果作为html标签的font-size值。 布局中使用rem作为单位。
- [FlipClock](http://www.flipclockjs.com/) - FlipClock.js 是一个制作精美时钟，定时器和倒计时的 jQuery 插件，并且可以完全通过 CSS 进行定制。有设置为自动启动，存在多种方法控制（启动，停止，getTime，setTime..），支持回调函数，此外，它还有一个全功能的API，能够进一步扩展功能。
- [iosSelect](http://zhoushengfe.com/iosselect/website/index.html) - 仿IOS端选择器插件，支持日期、地区等
- [移动端滑动插件better-scroll](http://ustbhuangyi.github.io/better-scroll/doc/zh-hans/#better-scroll) - better-scroll 是一款重点解决移动端（已支持 PC）各种滚动场景需求的插件。better-scroll 是基于原生 JS 实现的，不依赖任何框架。它编译后的代码大小是 63kb，压缩后是 35kb，gzip 后仅有 9kb，是一款非常轻量的 JS lib。
- [fastclick](https://majing.io/posts/10000007721218) - 移动设备上的浏览器默认会在用户点击屏幕大约延迟300毫秒后才会触发点击事件，这是为了检查用户是否在做双击。为了能够立即响应用户的点击事件，才有了FastClick。
<h5 id="mobile">其他类插件</h5>

- [onepage-scroll](https://github.com/peachananr/onepage-scroll) - 依赖 jQuery 的单页滚动库，和 [fullPage](http://alvarotrigo.com/fullPage/) 类似
- [videojs](http://videojs.com/) - 当下视频需求都用上```<video>```鸟 样式和交互统一的问题交给 videojs 搞定:)
- [clipboard](http://zenorocha.github.io/clipboard.js/) - 仅 2KB 大小，搞定剪贴板功能，屌不屌~ 但是，Safari 不支持...


<h2 id="read">精选阅读</h2>

<h3 id="fedev">前端技术</h3>

- [ECMAScript 6入门](http://es6.ruanyifeng.com/) - 阮一峰大神所著，一本开源的JS教程 全面介绍 ECMAScript 6新引入的语法特性
- [ReactWebpackCookBook](https://fakefish.github.io/react-webpack-cookbook/index.html) - 此书会引导读者是进入```React```和```Webpack```的世界。 俩都是非常前沿的技术，同时使用会更有趣。
- [ReactNative 学习指南](https://github.com/ele828/react-native-guide) - 新玩意层出不穷... 对于能持续学习的童鞋，这是个美好的时代
- [移动前端入门](http://gold.xitu.io/entry/56c29abfa34131005b8cb1f3) - 入门价值高，移动方向常见问题的较好总结
- [GulpBook](https://github.com/nimojs/gulp-book) - Gulp 是基于 Node 实现 Web 前端自动化开发的工具

<h3 id="node_read">Node 学习资料</h3>

- [Node.js 中文资料导航](https://github.com/youyudehexie/node123) - Node 的中文资料导航，```start1300+```
- [从零开始 NodeJS 系列文章](http://blog.fens.me/series-nodejs/) - 基本上每一篇都看过，强烈推荐
- [Node.js 包教不包会](http://nqdeng.github.io/7-days-nodejs/) - 值得阅读，看完绝不用买书鸟
- [七天学会 NodeJS](https://github.com/alsotang/node-lessons) - 劳资还没看，不过看目录还不错:)
- [Style Guide](https://github.com/dead-horse/node-style-guide) - 这是一份关于如何写出一致且美观的 ```Node``` 代码的风格指南
- [koa实战](http://book.apebook.org/minghe/koa-action/index.html) - “[明河](https://github.com/minghe)出品”这四字已经说明一切。PS：正在连载中
- [stream-handbook](https://github.com/jabez128/stream-handbook) - 如果学习 NodeJS，那么流一定是需要掌握的概念

<h3 id="otherdev">其他技术</h3>
- [微信小程序开发资源汇总](https://github.com/justjavac/awesome-wechat-weapp) - 天津第一程出品。微信小程序开发资源汇总。


以下是 [@拔赤](http://weibo.com/jayli) 总结的前端技能图：
![拔赤总结的前端技能图](https://raw.githubusercontent.com/nieweidong/fetool/master/img/fe.jpg)

---

**[⬆ 返回顶部](#前端工具)**
