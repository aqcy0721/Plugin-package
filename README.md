7/4/2019 12:35:08 AM # 前端工具 

聚名网前端工具，小组成员上传或者更新时做好commit

---

## 目录
- [插件](#plugins)
  - [功能插件](#features)
     - [弹出层](#layer)
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


功能插件
----------
### 弹出层

#### [layer](http://layer.layui.com/?alone)

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

> [点击下载](http://www.chaoyong666.com/js/layer_pc.zip)，想了解更多，可以去[官方文档](http://layer.layui.com/)找到

----------

#### [Layer For Mobile](http://layer.layui.com/mobile/) - 适用于移动端

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
> [点击下载](http://www.chaoyong666.com/js/layer_mobile.zip)，想了解更多，可以去[官方文档](http://layer.layui.com/mobile/api.html)找到

----------

### 上拉加载，下拉刷新

#### [Mescroll](http://www.mescroll.com/) - 精致的下拉刷新和上拉加载js框架，原生js，不依赖jquery，zepto，支持vue，一套代码多端运行

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
       noMoreSize: 5, 
       toTop: {
          //回到顶部按钮
          src: "../img/mescroll-totop.png", //图片路径,默认null,支持网络图
          offset: 1000 //列表滚动1000px才显示回到顶部按钮	
       },
	   empty: {
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

         //方法一(推荐): 后台接口有返回列表的总页数 totalPage
         //必传参数(当前页的数据个数, 总页数)
         //mescroll.endByPage(curPageData.length, totalPage);

         //方法二(推荐): 后台接口有返回列表的总数据量 totalSize
         //必传参数(当前页的数据个数, 总数据量)
         //mescroll.endBySize(curPageData.length, totalSize);

         //方法三(推荐): 您有其他方式知道是否有下一页 hasNext
         //必传参数(当前页的数据个数, 是否有下一页true/false)
         //mescroll.endSuccess(curPageData.length, hasNext);

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
> [点击下载](http://www.chaoyong666.com/js/mescroll.zip)，想了解更多，可以去[官方文档](http://www.mescroll.com/api.html?v=190725)找到

----------

### 上传

#### [jQuery File Upload](http://www.jq22.com/jquery-info230) -支持多文件上传、取消、删除，上传前缩略图预览、列表显示图片大小，支持上传进度条显示；支持各种动态语言开发的服务器端。

> **快速入门**
```javascript
引入依赖库
<script src="//ajax.googleapis.com/ajax/libs/jquery/1.8.3/jquery.min.js"></script><!-- 基础库 -->
<script src="js/vendor/jquery.ui.widget.js"></script><!-- 基于 iframe 文件上传的 jQuery Ajax 传输插件，通过隐藏的 iframe 来实现传输 -->
<script src="js/jquery.iframe-transport.js"></script>
<script src="js/jquery.fileupload.js"></script>

$(function () {
   $('#fileupload').fileupload({
      dataType: 'json',
      add: function (e, data) { //可以通过按钮点击事件来触发上传
         data.context = $('<button/>').text('Upload')
         .appendTo(document.body)
         .click(function () {
            $(this).replaceWith($('<p/>').text('Uploading...'));
            data.submit();
         });
      },
      done: function (e, data) {
         $.each(data.result.files, function (index, file) {
            $('<p/>').text(file.name).appendTo(document.body);
         });
      },
      progressall: function (e, data) { //进度条
         var progress = parseInt(data.loaded / data.total * 100, 10);
         $('#progress .bar').css(
           'width',
            progress + '%'
         );
      }
   });
});
```
![](https://i.imgur.com/5z0iR3C.jpg)
> [点击下载](http://www.chaoyong666.com/js/jQuery-File-Upload-master.zip)，想了解更多，可以去[官方文档](https://github.com/blueimp/jQuery-File-Upload)找到

----------

#### [zyupload](http://www.jq22.com/jquery-info14213) - PHP支持拖拽和裁剪的一款上传插件：zyupload。在js里面可以自定义高度和宽度，类型，远程上传地址等。

> **快速入门**
```javascript

引入依赖库
<script src="jQuery的路径"></script>
<link rel="stylesheet" href="zyupload.css的路径" type="text/css">
<script type="text/javascript" src="zyupload.js路径"></script>

$("#zyupload").zyUpload({
    width: "650px", // 宽度    
    height: "400px", // 宽度     
    itemWidth: "140px", // 文件项的宽度    
    itemHeight: "115px", // 文件项的高度    
    url: "./up.php", // 上传文件的路径    
    fileType: ["jpg", "png", "txt", "js"], // 上传文件的类型    
    fileSize: 51200000, // 上传文件的大小    
    multiple: true, // 是否可以多个文件上传     
    dragDrop: true, // 是否可以拖动上传文件    
    tailor: true, // 是否可以裁剪图片     
    del: true, // 是否可以删除文件     
    finishDel: false, // 是否在上传文件完成后删除预览     
    /* 外部获得的回调接口 */
    onSelect: function(selectFiles, allFiles) { // 选择文件的回调方法  
        selectFile: 当前选中的文件
        allFiles: 还没上传的全部文件
        console.info("当前选择了以下文件：");console.info(selectFiles);
    },
    onDelete: function(file, files) { // 删除一个文件的回调方法 file:当前删除的文件 
        files: 删除之后的文件
        console.info("当前删除了此文件：");
        console.info(file.name);
    },
    onSuccess: function(file, response) { // 文件上传成功的回调方法     
        console.info("此文件上传成功：");
        console.info(file.name);
        console.info("此文件上传到服务器地址：");
        console.info(response);
        $("#uploadInf").append("<p>上传成功，文件地址是：" + response + "</p>");
    },
    onFailure: function(file, response) { // 文件上传失败的回调方法        
        console.info("此文件上传失败：");
        console.info(file.name);
    },
    onComplete: function(response) { // 上传完成的回调方法        
        console.info("文件上传完成");
        console.info(response);
    }
});
```
![](https://i.imgur.com/vdqyH23.jpg)
> [点击下载](http://www.chaoyong666.com/js/zyupload.zip)，想了解更多，可以去[官方文档](http://www.jq22.com/jquery-info14213)找到

----------

### 轮播图

#### [Swiper](https://www.swiper.com.cn/) - 纯javascript打造的滑动特效插件，面向手机、平板电脑等移动终端，版本：4.0

> **快速入门**
```html
<!DOCTYPE html>
<html>
   <head>
   ...引入js与css
   <link rel="stylesheet" href="dist/css/swiper.min.css">
   <script src="dist/js/swiper.min.js"></script>
</head>
<body>
   <div class="swiper-container">
      <div class="swiper-wrapper">
         <div class="swiper-slide">Slide 1</div>
         <div class="swiper-slide">Slide 2</div>
         <div class="swiper-slide">Slide 3</div>
      </div>
      <!-- 如果需要分页器 -->
      <div class="swiper-pagination"></div>
    
      <!-- 如果需要导航按钮 -->
      <div class="swiper-button-prev"></div>
      <div class="swiper-button-next"></div>
    
      <!-- 如果需要滚动条 -->
      <div class="swiper-scrollbar"></div>
   </div>
   导航等组件可以放在container之外
</body>
</html>
```
```javascript
var mySwiper = new Swiper ('.swiper-container', {
    direction: 'vertical', // 垂直切换选项
    loop: true, // 循环模式选项
    
    // 如果需要分页器
    pagination: {
      el: '.swiper-pagination',
    },
    
    // 如果需要前进后退按钮
    navigation: {
      nextEl: '.swiper-button-next',
      prevEl: '.swiper-button-prev',
    },
    
    // 如果需要滚动条
    scrollbar: {
      el: '.swiper-scrollbar',
    },
  })    
```
> [点击下载](http://www.chaoyong666.com/js/swiper-4.5.0.zip)，想了解更多，可以去[官方文档](https://www.swiper.com.cn/usage/index.html)找到

----------

### 表单验证

#### [myvali](http://www.jq22.com/jquery-info18673) - 基于jquery封装的表单验证插件

> **快速入门**

```javascript
<script src="jQuery的路径"></script>
<script type="text/javascript" src="myvali.js路径"></script>
$.myvali({
    myform: ".form2", //表单id
    mybtn: ".btn", //提交表单按钮id 
    myVali: ".vali", //input父盒子的class，可自定义类名
    Required: ".Required", //验证必填选项，值为Required,input自己加class
    RequiredTps: ["不能为空!!!"], //只验证不为空提示
    Requireds: ".Requireds", //验证必填不同提示，值为Requireds,input自己加class
    reqtps: ".reqtps", //验证不为空不同提示,input父盒子的class,可自定义类名
    Reqlength: [
        [2, 4]
    ], //只验证不为空,设置最小长度和最大长度
    ReqlengthTps: ["+不为空1"], //验证不为空长度提示
    RequiredsTps: ["这是自定义提示1"], //默认提示
    myNuber: ".nub", //数字验证
    myNuberlength: [5, 10], //数字长度
    myNameNuber: "QQ", //数字提示
    chinese: ".chinese", //中文验证id
    chinesetps: {
        minLength: 2, //最小长度
        maxLength: 4, //最大长度
        tps: "姓名", //提示
    },
    myName: ".uersname", //用户名id或class
    nameIsServer: true, //用户名是否要与数据库验证，true为是，默认false为否
    nameIsServerUrl: ["1.php"], //用户名与数据库验证的路径。
    nameIsServerType: "post", //用户名以什么方式提交
    nameIsServerDType: "json", //用户名以什么格式提交
    myPassword: ".pasw", //密码id或class
    myPasswordMinLength: 6, //密码最小长度，不写默认长度6
    myPasswordMaxLength: 16, //密码最大长度，不写默认长度16
    myConfirmPassword: ".pasws", //确认密码id或class
    myPhone: ".phone", //手机号id或class
    phoneIsServer: true, //手机号是否与数据库验证，true为是，默认false为否
    phoneIsServerUrl: ["1.php"], //手机号与数据库验证的路径
    phoneIsServerType: "post", //以什么方式提交
    phoneIsServerDType: "json", //以什么格式提交
    isPhoneCode: true, //开启手机短信验证，true开启，默认false不开启(此项功能与myPhone配合验证)
    phoneCodeBtn: ".codebtn", //发送手机验证码id或class（按钮）
    count: 30, //发送短信验证码倒计时，默认60s（按钮）
    codeBtnCol1: ["rgb(150, 150, 150)"], //短信验证码倒计时（按钮，通过验证前）颜色
    codeBtnCol2: ["#333"], //短信验证码倒计时（按钮，通过验证后）颜色
    isPhoneCodeUrl: ["1.php"], //发送手机验证码与数据库验证的路径（按钮）
    isPhoneCodeType: "post", //以什么方式提交（按钮）
    isPhoneCodeDType: "json", //以什么格式提交（按钮）
    myPhone1: "#v", //修改手机号(原手机号用这个验证)id或class
    phoneIsServer1: false, //手机号是否与数据库验证，true为是，默认false为否
    phoneIsServerUrl1: ["1.php"], //手机号与数据库验证的路径
    phoneIsServerType1: "post", //以什么方式提交
    phoneIsServerDType1: "json", //以什么格式提交
    phoneCodeInput: ".phcode", //短信验证码id或class（输入框）
    phoneCodeInputUrl: ["1.php"], //短信验证码与数据库验证的路径（输入框）
    phoneCodeInputType: "post", //以什么方式提交（输入框）
    phoneCodeInputDType: "json", //以什么格式提交（输入框）
    myMailbox: ".eal", //邮箱id或class
    mailboxIsServer: false, //邮箱是否要与数据库验证，默认false为否
    mailboxIsServerUrl: ["1.php"], //邮箱与数据库验证的路径
    mailboxIsServerType: "post", //以什么方式提交
    mailboxIsServerDType: "json", //以什么格式提交
    myCard: ".cid", //身份证验证id或class
    myCode: "#v", //验证码id或class
    CodeIsServerUrl: ["1.php"], //验证码与数据库验证的路径
    CodeIsServerType: "post", //以什么方式提交
    CodeIsServerDType: "json", //以什么格式提交
    PwdStrong: true, //密码强度验证，默认false不开启，true开启
    isStrongTps: ["弱", "中", "强"], //密码强度提示，可自定义提示
    myNameMinLength: 3, //用户名最小长度，不写默认长度3
    myNameMaxLength: 12, //用户名最大长度，不写默认长度12
    myNameMinLength2: 3, //昵称最小长度，不写默认长度3
    myNameMaxLength2: 12, //昵称最大长度，不写默认长度12
    corrCol: "#4E7504", //设置正确提示文字的颜色，不设置默认绿色
    errCol: "red", //设置错误提示文字的颜色，不设置默认红色
})  
```
![](https://i.imgur.com/F0XWyIV.jpg)
> [点击下载](http://www.chaoyong666.com/js/myvali.zip)，想了解更多，可以去[官方文档](http://www.jq22.com/jquery-info18673)找到

----------

### 日期控件

#### [jedate](http://www.jemui.com/uidoc/jedate.html) - 基于jquery封装的表单验证插件

> **快速入门**

```javascript
引入js与css
<link type="text/css" rel="stylesheet" href="skin/jedate.css">
<script type="text/javascript" src="src/jedate.js"></script>

//DOM设置
<input type="text" class="jeinput" id="starttime">

//初始化
jeDate("#starttime",{
    festival:true,
    minDate:"1900-01-01",              //最小日期
    maxDate:"2099-12-31",              //最大日期
    method:{
        choose:function (params) {
            
        }
    },
    format: "YYYY-MM-DD hh:mm:ss"
});  

```
> [点击下载](http://www.chaoyong666.com/js/jedate-6.5.0.zip)，想了解更多，可以去[官方文档](http://www.jemui.com/uidoc/jedate.html)找到

----------

### 图表类插件

#### [ECharts](http://echarts.baidu.com/index.html) - 支持的图表展示非常之多

> **快速入门**

```javascript
引入js与css
<script src="echarts.min.js"></script>

//为 ECharts 准备一个具备大小（宽高）的 DOM
<div id="main" style="width: 600px;height:400px;"></div>

// 基于准备好的dom，初始化echarts实例
var myChart = echarts.init(document.getElementById('main'));

// 指定图表的配置项和数据
var option = {
    title: {
        text: 'ECharts 入门示例'
    },
    tooltip: {},
    legend: {
        data:['销量']
    },
    xAxis: {
        data: ["衬衫","羊毛衫","雪纺衫","裤子","高跟鞋","袜子"]
    },
    yAxis: {},
    series: [{
        name: '销量',
        type: 'bar',
        data: [5, 20, 36, 10, 10, 20]
    }]
};

// 使用刚指定的配置项和数据显示图表。
myChart.setOption(option);
});  

```
> [点击下载](http://www.chaoyong666.com/js/echarts-4.2.1.zip)，想了解更多，可以去[官方文档](https://www.echartsjs.com/tutorial.html#5%20%E5%88%86%E9%92%9F%E4%B8%8A%E6%89%8B%20ECharts)找到

----------

### 拖拽类插件

#### [Sortable](https://github.com/RubaXa/Sortable) - 拖拽神器

> **快速入门**

```javascript
npm下载
$ npm install sortablejs --save

引入js
import Sortable from 'sortablejs';

<ul id="items">
	<li>item 1</li>
	<li>item 2</li>
	<li>item 3</li>
</ul>

var el = document.getElementById('items');
var sortable = Sortable.create(el);

// 基本配置
var sortable = new Sortable(el, {
	group: "name",  // or { name: "...", pull: [true, false, 'clone', array], put: [true, false, array] }
	sort: true,  // sorting inside list
	delay: 0, // time in milliseconds to define when the sorting should start
	delayOnTouchOnly: false, // only delay if user is using touch
	touchStartThreshold: 0, // px, how many pixels the point should move before cancelling a delayed drag event
	disabled: false, // Disables the sortable if set to true.
	store: null,  // @see Store
	animation: 150,  // ms, animation speed moving items when sorting, `0` — without animation
	easing: "cubic-bezier(1, 0, 0, 1)", // Easing for animation. Defaults to null. See https://easings.net/ for examples.
	handle: ".my-handle",  // Drag handle selector within list items
	filter: ".ignore-elements",  // Selectors that do not lead to dragging (String or Function)
	preventOnFilter: true, // Call `event.preventDefault()` when triggered `filter`
	draggable: ".item",  // Specifies which items inside the element should be draggable

	dataIdAttr: 'data-id',

	ghostClass: "sortable-ghost",  // Class name for the drop placeholder
	chosenClass: "sortable-chosen",  // Class name for the chosen item
	dragClass: "sortable-drag",  // Class name for the dragging item

	swapThreshold: 1, // Threshold of the swap zone
	invertSwap: false, // Will always use inverted swap zone if set to true
	invertedSwapThreshold: 1, // Threshold of the inverted swap zone (will be set to swapThreshold value by default)
	direction: 'horizontal', // Direction of Sortable (will be detected automatically if not given)

	forceFallback: false,  // ignore the HTML5 DnD behaviour and force the fallback to kick in

	fallbackClass: "sortable-fallback",  // Class name for the cloned DOM Element when using forceFallback
	fallbackOnBody: false,  // Appends the cloned DOM Element into the Document's Body
	fallbackTolerance: 0, // Specify in pixels how far the mouse should move before it's considered as a drag.

	dragoverBubble: false,
	removeCloneOnHide: true, // Remove the clone element when it is not showing, rather than just hiding it
	emptyInsertThreshold: 5, // px, distance mouse must be from empty sortable to insert drag element into it


	setData: function (/** DataTransfer */dataTransfer, /** HTMLElement*/dragEl) {
		
	},

	// Element is chosen
	onChoose: function (/**Event*/evt) {
		
	},

	// Element is unchosen
	onUnchoose: function(/**Event*/evt) {
		
	},


	onStart: function (/**Event*/evt) {
		
	},

	// Element dragging ended
	onEnd: function (/**Event*/evt) {
		
	},

	// Element is dropped into the list from another list
	onAdd: function (/**Event*/evt) {
		
	},

	// Changed sorting within list
	onUpdate: function (/**Event*/evt) {
		
	},

	// Called by any change to the list (add / update / remove)
	onSort: function (/**Event*/evt) {
		
	},

	// Element is removed from the list into another list
	onRemove: function (/**Event*/evt) {
		
	},

	// Attempt to drag a filtered element
	onFilter: function (/**Event*/evt) {
		
	},

	// Event when you move an item in the list or between lists
	onMove: function (/**Event*/evt, /**Event*/originalEvent) {
		
	},

	// Called when creating a clone of element
	onClone: function (/**Event*/evt) {
		
	},

	// Called when dragging element changes position
	onChange: function(/**Event*/evt) {
		
	}
});

```
> [点击下载](http://www.chaoyong666.com/js/sortablejs.zip)，想了解更多，可以去[官方文档](https://github.com/SortableJS/Sortable)找到

----------

### 省市联动

#### [jquery.cityselect](http://www.jq22.com/yanshi16052) - jQuery+JSON的省市三级、二级联动插件

> **快速入门**

```javascript
引入js
<script src="http://www.jq22.com/jquery/jquery-1.10.2.js"></script>
<script type="text/javascript" src="js/jquery.cityselect.js"></script>

<div id="city_1">
	<select class="prov"></select>
	<select class="city" disabled="disabled"></select>
</div>

// 基于准备好的dom，初始化echarts实例
$("#city_1").citySelect({nodata:"none",required:false}); 
```
![](https://i.imgur.com/rFux4a6.jpg)
> [点击下载](http://www.chaoyong666.com/js/jquery.cityselect.zip)，想了解更多，可以去[官方文档](http://www.jq22.com/yanshi16052)找到

----------

### 3D库

#### [three.js](https://github.com/mrdoob/three.js) - JavaScript 3D 库

> **快速入门**

```javascript
引入js
<script src="js/three.min.js"></script>

var camera, scene, renderer;
var geometry, material, mesh;

init();
animate();

function init() {

	camera = new THREE.PerspectiveCamera( 70, window.innerWidth / window.innerHeight, 0.01, 10 );
	camera.position.z = 1;

	scene = new THREE.Scene();

	geometry = new THREE.BoxGeometry( 0.2, 0.2, 0.2 );
	material = new THREE.MeshNormalMaterial();

	mesh = new THREE.Mesh( geometry, material );
	scene.add( mesh );

	renderer = new THREE.WebGLRenderer( { antialias: true } );
	renderer.setSize( window.innerWidth, window.innerHeight );
	document.body.appendChild( renderer.domElement );

}

function animate() {

	requestAnimationFrame( animate );

	mesh.rotation.x += 0.01;
	mesh.rotation.y += 0.02;

	renderer.render( scene, camera );

}
```
> 想了解更多，可以去[官方文档](https://github.com/mrdoob/three.js)找到+

----------

### HTML生成图片

#### [html2canvas](https://github.com/niklasvh/html2+)+[canvas2Image](https://github.com/randreucetti/canvas2image) - 使用场景就是“动态生成的HTML可以长按保存为图片”。

> **快速入门**

```javascript
引入js
<script src="http://www.jq22.com/jquery/jquery-1.7.2.js"></script>
<script src="http://img.chaicp.com/img/html2canvas.min.js"></script>

<div id="wrap">
	...
</div>

html2canvas($("#wrap"), {
 	useCORS: true,
     onrendered: function (canvas) {
         var url = canvas.toDataURL();
          //以下代码为下载此图片功能
         var triggerDownload = $("<a>").attr("href", url).attr("download", "xxx.png").appendTo("body");
       },
       background: "#000"
});
```
> [点击下载html2cavas](http://www.chaoyong666.com/js/html2canvas-master.zip)，[点击下载canvas2image](http://www.chaoyong666.com/js/canvas2image-master.zip)，想了解更多，可以去[官方文档](https://github.com/niklasvh/html2canvas)找到

----------

### 懒加载

#### [jquery.lazyload](http://www.jq22.com/yanshi390) - 使用延迟加载在可提高网页下载速度。在某些情况下，它也能帮助减轻服务器负载。

> **快速入门**

```javascript
引入js
<script src="jquery-1.11.0.min.js"></script>
<script src="jquery.lazyload.js?v=1.9.1"></script>

<img class="lazy" data-original="img/bmw_m1_hood.jpg">

$(function() {
   $("img.lazy").lazyload({effect: "fadeIn"});
});
```
> [点击下载](http://www.chaoyong666.com/js/jquery.lazyload.zip)，想了解更多，可以去[官方文档](http://www.jq22.com/yanshi390)找到

----------

移动端插件
----------

### [adaptive.js](https://github.com/Vibing/adaptive) - 借鉴手淘方案，adaptive.js将整个页面宽度平均分成10份，以clineWidth / 10的结果作为html标签的font-size值。 布局中使用rem作为单位。

> **快速入门**
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="initial-scale=1, maximum-scale=1,minimum-scale=1, user-scalable=no, minimal-ui">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black">
    <title>template</title>
    <script src="adaptive.min.js"></script>
    <style>
        .wrap{
            position: relative;
            width: 10rem;
            margin:0 auto;
        }
    </style>
    </head>
<body>
<div class="wrap">

</div>
</body>
</html>
```
> [点击下载](http://www.chaoyong666.com/js/adaptive-master.zip)，想了解更多，可以去[官方文档](https://github.com/Vibing/adaptive)找到

----------

### [FlipClock](http://www.flipclockjs.com/) - FlipClock.js 是一个制作精美时钟，定时器和倒计时的 jQuery 插件，并且可以完全通过 CSS 进行定制。有设置为自动启动，存在多种方法控制（启动，停止，getTime，setTime..），支持回调函数，此外，它还有一个全功能的API，能够进一步扩展功能。

> **快速入门**
```html
<html>
	<head>
		<link rel="stylesheet" href="/assets/css/flipclock.css">
	</head>
	<body>
		<div class="your-clock"></div>
		
		<script src="/assets/js/libs/jquery.js"></script>
		<script src="/assets/js/flipclock/flipclock.min.js"></script>
	</body>
</html>
```
```javascript
var clock = $('.your-clock').FlipClock({
// ... your options here
});
var clock = new FlipClock($('.your-clock'), {
// ... your options here
});
```
> [点击下载](http://www.chaoyong666.com/js/FlipClock-master.zip)，想了解更多，可以去[官方文档](http://www.flipclockjs.com/)找到

----------

### [iosSelect](http://zhoushengfe.com/iosselect/website/index.html) - 仿IOS端选择器插件，支持日期、地区等

> **快速入门**
```javascript
<link rel="stylesheet" href="/static/css/iosSelect.css">
<script type="text/javascript" src="/static/js/iosSelect.js"></script>

var showDom = document.querySelector('#showDom');// 绑定一个触发元素
var valDom = document.querySelector('#valDom');  // 绑定一个存储结果的元素
showDom.addEventListener('click', function () {  // 添加监听事件
    var val = showDom.dataset['id'];             // 获取元素的data-id属性值
    var title = showDom.dataset['value'];        // 获取元素的data-value属性值
  // 实例化组件
    var example = new IosSelect(1,               // 第一个参数为级联层级，演示为1
        [[{'id': '10001', 'value': '演示数据1'},{'id': '10002', 'value': '演示数据2'}]],                             // 演示数据
        {
            container: '.container',             // 容器class
            title: '演示标题',                    // 标题
            itemHeight: 50,                      // 每个元素的高度
            itemShowCount: 3,                    // 每一列显示元素个数，超出将隐藏
            oneLevelId: val,                     // 第一级默认值
            callback: function (selectOneObj) {  // 用户确认选择后的回调函数
                valDom.value = selectOneObj.id;
                showDom.innerHTML = selectOneObj.value;
                showDom.dataset['id'] = selectOneObj.id;
                showDom.dataset['value'] = selectOneObj.value;
            }
    });
});
```
> [点击下载](http://www.chaoyong666.com/js/iosselect.zip)，想了解更多，可以去[官方文档](http://zhoushengfe.com/iosselect/website/index.html)找到

----------

### [better-scroll](http://ustbhuangyi.github.io/better-scroll/doc/zh-hans/#better-scroll) - better-scroll 是一款重点解决移动端（已支持 PC）各种滚动场景需求的插件。better-scroll 是基于原生 JS 实现的，不依赖任何框架。它编译后的代码大小是 63kb，压缩后是 35kb，gzip 后仅有 9kb，是一款非常轻量的 JS lib。

> **快速入门**
```html
<div class="wrapper">
  <ul class="content">
    <li>...</li>
    <li>...</li>
    ...
  </ul>
  <!-- 这里可以放一些其它的 DOM，但不会影响滚动 -->
</div>
```
```javascript
import BScroll from 'better-scroll'
let wrapper = document.querySelector('.wrapper')
let scroll = new BScroll(wrapper)
```
> [点击下载](http://www.chaoyong666.com/js/better-scroll.zip)，想了解更多，可以去[官方文档](http://ustbhuangyi.github.io/better-scroll/doc/zh-hans/#%E8%B5%B7%E6%AD%A5)找到

----------

### [fastclick](https://majing.io/posts/10000007721218) - 移动设备上的浏览器默认会在用户点击屏幕大约延迟300毫秒后才会触发点击事件，这是为了检查用户是否在做双击。为了能够立即响应用户的点击事件，才有了FastClick。

> **快速入门**
```javascript
//纯Javascript版
<script type='application/javascript' src='/path/to/fastclick.js'></script>
document.addEventListener('DOMContentLoaded', function() {
		FastClick.attach(document.body);
	}, false);
```
```javascript
//Common JS的模块系统方式
npm install fastclick
var attachFastClick = require('fastclick');
attachFastClick(document.body);
```
> [点击下载](http://www.chaoyong666.com/js/fastclick.zip)，想了解更多，可以去[官方文档](https://majing.io/posts/10000007721218)找到

----------

其他类插件
----------

### [onepage-scroll](https://github.com/peachananr/onepage-scroll) - 依赖 jQuery 的单页滚动库，和 [fullPage](http://alvarotrigo.com/fullPage/) 类似

> **快速入门**
```html
<body>
  ...
  <div class="main">
    <section>...</section>
    <section>...</section>
    ...
  </div>
  ...
</body>
```
```javascript
$(".main").onepage_scroll({
   sectionContainer: "section",
   easing: "ease",
   animationTime: 1000,
   pagination: true,
   updateURL: false,
   beforeMove: function(index) {},
   afterMove: function(index) {},
   loop: false, 
   keyboard: true,
   responsiveFallback: false,
   direction: "vertical"
});
```
> [点击下载](http://www.chaoyong666.com/js/onepage-scroll-master.zip)，想了解更多，可以去[官方文档](http://www.thepetedesign.com/demos/onepage_scroll_demo.html)找到

----------

### [clipboard](https://clipboardjs.com/) - 仅 2KB 大小，搞定剪贴板功能,但是，Safari 不支持...

> **快速入门**
```html
<!-- Target -->
<input id="foo" value="https://github.com/zenorocha/clipboard.js.git">

<!-- Trigger -->
<button class="btn" data-clipboard-target="#foo">
    <img src="assets/clippy.svg" alt="Copy to clipboard">
</button>
```
![兼容性](https://i.imgur.com/R3wDWUz.jpg)
> [点击下载](http://www.chaoyong666.com/js/clipboard.zip)，想了解更多，可以去[官方文档](https://clipboardjs.com/)找到

----------

<h2 id="read">精选阅读</h2>

<h3 id="fedev">前端技术</h3>

- [ECMAScript 6入门](http://es6.ruanyifeng.com/) - 阮一峰大神所著，一本开源的JS教程 全面介绍 ECMAScript 6新引入的语法特性
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
