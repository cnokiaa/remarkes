# 参考

##### css自动换行

    word-break: break-all;
    word-wrap: break-word;
    white-space: pre-wrap;
    white-space: -moz-pre-wrap;
    white-space: -pre-wrap;
    white-space: -o-pre-wrap;

#### 文字超过显示为省略号        
    -o-text-overflow:ellipsis;
    white-space:nowrap;
    text-overflow:ellipsis;
    overflow:hidden;

#### css隐藏文字
    text-indent: -9999px;display: block;

#### marquee滚动
    marquee

#### pointer-events鼠标监听
    pointer-events

#### textarea不给拉伸css
    resize: none;

#### ie6下处理png图片不透明css
    _background:none;
    _filter:progid:DXImageTransform.Microsoft.AlphaImageLoader(src='../img/iconNext.png');_

#### css设置阴影效果
    box-shadow: 0 1px 5px rgba(110,110,110,.7);

#### css3平滑地过渡效果
    -webkit-transition: all .3s ease;
    transition: all .3s ease;

#### 设置背景透明css

    filter: progid:DXImageTransform.Microsoft.gradient(enabled='true', startColorstr='#BFFFFFFF', endColorstr='#BFFFFFFF');
    background: rgba(255,255,255,.01);
    filter: alpha(opacity=40);

##### 线性渐变css

    -webkit-gradient(linear,0% 0%, 0% 100%, from(#999999), to(#333333), color-stop(0.5,#336600));
    -moz-linear-gradient(0% 0% 270deg, #999999,#333333, #336600 50%)

#### css3 transform
`-webkit-transform/-moz-transform:{rotate旋转,skew倾斜,scale放大缩小}`

* CSS3 transition 属性

      transition ：[
    	<transition-property :
    		none | all(所有属性都将获得过渡效果) | property(定义应用过渡效果的CSS属性名称列表，列表以逗号分隔);
    	>
    	<transition-duration : time(完成过渡效果需要多少秒或毫秒);>
    	<transition-timing-function :
    		linear(以相同速度开始至结束的过渡效果) |
    		ease(慢速开始，然后变快，然后慢速结束的过渡效果) |
    		ease-in(以慢速开始的过渡效果) |
    		ease-out(以慢速结束的过渡效果) |
    		ease-in-out(以慢速开始和结束的过渡效果) |
    		cubic-bezier(n,n,n,n) (中定义自己的值(0,0,1,1));
    	>
    	<transition-delay : time(过渡效果何时开始);>]

* rotate旋转10度

      -webkit-transform:rotate(10deg);
      -moz-transform:rotate(10deg);

* skew倾斜20度

      -webkit-transform:skew(20deg);
      -moz-transform:skew(20deg);

* scale放大1.5倍，缩小为负数

      -webkit-transform:scale(1.5);
      -moz-transform:scale(1.5);

* translate上下左右移动，左下为负

      -webkit-transform:translate(120px,0);
      -moz-transform:translate(120px,0);

#### transition的小实例
* 逐渐变慢效果

      background: #f36;
      -webkit-transition: all 5s ease 0.3s;

* 加速效果
      -webkit-transition: all 3s ease-in 0.5s;

* 减速效果
      -webkit-transition: all 5s ease-out 0s;

* 先加速然后减速效果

      -webkit-transition: all 1s ease-in-out 2s;  
* 匀速效果

      -webkit-transition: all 6s linear 0s;  

* 该值允许你去自定义一个时间曲线效果

      -webkit-transition: all 4s cubic-bezier 1s;
#### iframe

      <frameborder="0" scrolling="no" width="" height="">

* js设置iframe高度

      function iFrameHeight(iname) {   
    	var ifm= document.getElementById(iname);   
    	var subWeb = document.frames ? document.frames[iname].document : ifm.contentDocument;   
    	if(ifm != null && subWeb != null) {
    	   ifm.height = subWeb.body.scrollHeight;
    	}   
      }  
#### css实现图片变成灰色，鼠标经过变成彩色（ie6-9，chrome，Firefox）

	   .image-filter {
		  filter: url("data:image/svg+xml;utf8,<svg xmlns=\'http://www.w3.org/2000/svg\'><filter id=\'grayscale\'><feColorMatrix type=\'matrix\' values=\'0.3333 0.3333 0.3333 0 0 0.3333 0.3333 0.3333 0 0 0.3333 0.3333 0.3333 0 0 0 0 0 1 0\'/></filter></svg>#grayscale"); /* Firefox 3.5+ */
		  filter: gray; /* ie6-8 */
		  filter:progid:DXImageTransform.Microsoft.BasicImage(grayscale=1);/*ie6-9 */
		  filter: grayscale(100%); /* 未来浏览器 */
		  -webkit-filter: grayscale(100%); /* Chrome 19+ & Safari 6+ */
		  -webkit-transition: all 0.4s ease-in-out;
		  -webkit-transition: all 0.4s ease-in-out;
		  -moz-transition: all 0.4s ease-in-out;
		  transition: all 0.4s ease-in-out;
		  -webkit-transform: translateZ(0);
		}

	   .image-filter:hover {
    	  filter: none;
    	  -webkit-filter: grayscale(0%);
    	  -webkit-transition: all 0.2s ease-in-out;
    	  -webkit-transition: all 0.2s ease-in-out;
    	  -moz-transition: all 0.2s ease-in-out;
    	  transition: all 0.2s ease-in-out;
    	  -webkit-transform: translateZ(0);
	     }


#### 使用base64 img
不能与其他图片以CSS Sprite的形式存在，只能独行，
这类图片从诞生之日起，基本上很少被更新，
在网站中大规模使用，
这类图片的实际尺寸很小。

#### js实现拖动table的宽度

    function SortTable(id){
        this.init(id);
    }
    SortTable.prototype = {
    	data:[],
    	_table:null,
    	norder:[],
    	_moveOffset:0,
    	init:function(id) {
    		this._table = $("#"+id);
    		var trs = this._table.find("tbody tr");
    		var _this = this;
    		trs.each(function(){
    			var row = [];
    			$(this).children().each(function(){
    				row.push($(this).html());
    			});
    			_this.data.push(row);                
    		});            
    		var theads = this._table.find("thead tr").children();
    		var _this = this;            
    		theads.each(function(idl){
    			if($(this).attr("class") && $(this).attr("class").indexOf("order") >= 0) {
    				if($(this).children("a").length <= 0) {
    					var slink = $("<a href='javascript:'></a>");
    					slink.text($(this).text());
    					$(this).text("");
    					$(this).append(slink);
    				}
    				$(this).children("a").css({textDecoration:"underline",color:"#185b9e",cursor:"pointer"});
    				$(this).children("a").click(function(){
    					_this.sort(idl);
    				});
    			}
    			if(idl >= theads.length-1)
    				return;
    			//拖曳宽度初始化
    			var dra = $("<div></div>").appendTo(this);
    			dra.css({position:"absolute",width:"2px",float:"right",
    							borderLeft:this.style.borderLeft,
    							borderRight:this.style.borderRight,
    							cursor:"col-resize",backgroundColor:"#fff"});
    			dra.attr("index",idl);

    			var td = $(this);
    			var tdoffset = td.offset();
    			dra.css({height:td.height(),top:0,left:(tdoffset.left+td.width()+2)});
    			td.click(function(_e){
    				var et = _e?_e:event;
    				et.stopPropagation();
    				return false;
    			});
    			dra.mousedown(function(_event){
    				//alert(_event.pageX);
    				_this._moveOffset = {index:$(this).attr("index"),y:_event.pageY,x:_event.pageX,tdwidth:td.width(),ntdwidth:td.next().width()};
    			});
    			$(_this._table).mouseup(function(){
    				_this._moveOffset=0;
    			});
    			$(_this._table).mousemove(function(_event){


    				if(!_this._moveOffset)
    					return;
    				var _width = _event.pageX-_this._moveOffset.x;

    				var dratd = theads[_this._moveOffset.index];

    				$(dratd).css("width",_this._moveOffset.tdwidth+_width);
    				ntd = $(dratd).next();
    				ntd.css("width",_this._moveOffset.ntdwidth-_width);
    				var tdoffset = td.offset();
    				dra.css({height:td.height(),top:0,left:(tdoffset.left+td.width()+2)});
    			});
    		})
    	},
    	sort:function(index) {
    		var isOrder = true;            
    		while(isOrder) {
    			isOrder = false;
    			for(var i = 0;i < this.data.length-1;i++){                    
    				if(!this.norder[index]){                        
    					if(this.data[i][index] > this.data[i+1][index]){
    						var tmp = this.data[i];
    						this.data[i] = this.data[i+1];
    						this.data[i+1] = tmp;
    						isOrder = true;
    					}
    				}else{                        
    					if(this.data[i][index] < this.data[i+1][index]){
    						var tmp = this.data[i];
    						this.data[i] = this.data[i+1];
    						this.data[i+1] = tmp;
    						isOrder = true;
    					}
    				}
    			}
    		}
    		if(!this.norder[index])
    			this.norder[index] = true;
    		else
    			this.norder[index] = false;            
    		this.fillTable();
    	},
    	fillTable:function(){
    		var tbody = this._table.find("tbody")
    		tbody.children().remove();
    		for(var i = 0;i < this.data.length;i++){
    			var row = $("<tr></tr>").appendTo(tbody);
    			for(var j = 0; j < this.data[i].length; j++){                    
    				row.append("<td style='border:1px dotted silver'>"+ this.data[i][j] +"</td>");
    			}
    		}
    	}
    }    
    var mytable =  new SortTable("listSort");

#### 响应式布局400px-600px-1300px

    <meta name="viewport" content="width=device-width, initial-scale=1" >
    <link rel="stylesheet" type="text/css" media="screen and (min-width:600px) and (max-width:960px)" href="css/gt-600px-lt-960px.css">
    <!--当页面宽度大于等于600px且小于等于960px时，载入样式表gt-600px-lt-960px.css-->
    @media screen and (max-width: 1200px) {
    	.idd{width:100% !important;}
    }
    <!--[if lt IE 9]>
    	<script src="http://css3-mediaqueries-js.googlecode.com/svn/trunk/css3-mediaqueries.js"></script>
    <![endif]-->

    <!--[if lt IE 9]>
    <script>
    	var dd = document.documentElement.clientWidth;
    	if(dd<1200){
    		var url = "css/suit.css";
    		var link = document.createElement("link");  
    			link.rel = "stylesheet";  
    			link.type = "text/css";  
    			link.href = url;  
    			document.getElementsByTagName("head")[0].appendChild(link);
    	}
    </script>
    <![endif]-->

#### tab切换js

    $(this).addClass("catch").siblings().removeClass("catch");   //tab头
    $(b).eq($(this).index()).show().siblings(c).hide();			//切换显示隐藏的内容

#### 实现导航栏鼠标经过效果

    $bsmenul.bind({
      mouseover:function(){
      	x=$(this).position().left;
      	$bsmm.show();
      	$bsmm.animate({left:x},50);
      },
      mouseout:function(){
      	$bsmm.hide();
      }

    });		

#### 浏览器的文档模式

    怪异模式： <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">
    HTML4标准模式：
    <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">  
    <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Frameset//EN" "http://www.w3.org/TR/html4/frameset.dtd">
    XHTML1.0
    (1)过渡型（Transitional ）
    <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
    (2)严格型（Strict ）
    <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
    (3)框架型（Frameset ）
    <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Frameset//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-frameset.dtd">


#### 鼠标向上向滚动
    var scrollFunc=function(e){
        ee=e || window.event;
       if(e.wheelDelta){//IE/Opera/Chrome
            if(e.wheelDelta>0){//向上
            } else{//向下}
        }else if(e.detail){//Firefox
            if(e.detail>0){//向下}else{//向上}
        }  
    }
    /*注册事件*/
    if(isFirefox=navigator.userAgent.indexOf("Firefox")>0){  
    if(document.addEventListener){document.addEventListener('DOMMouseScroll',scrollFunc,false);}
    } else {
    document.onmousewheel=scrollFunc;//IE/Opera/Chrome
    }

#### 点击S外的其他地方隐藏
    document.onclick = function(e){
    	e = e || window.event;
    	var dom =  e.srcElement|| e.target;
    	if(dom.getElementById != "S" && $("#S").css("display") == "block") {
    		$("#OUTBANK").slideUp();
    	} 	
    };
    触发显示S中加，方法参数加e：
    e = e||window.event;		
    e.stopPropagation();
#### html空格占位符
    &#32; == 普通的英文半角空格

    &#160; == &nbsp; == &#xA0; == no-break space （普通的英文半角空格但不换行）

    &#12288; == 中文全角空格 （一个中文宽度）

    &#8194; == &ensp; == en空格 （半个中文宽度）

    &#8195; == &emsp; == em空格 （一个中文宽度）

    &#8197; == 四分之一em空格 （四分之一中文宽度）
#### html5头部声明
    <!DOCTYPE html>
    <html lang="zh-cmn-Hans">
    <head>
    <meta charset="utf-8">
    <meta name="viewport" content="initial-scale=1, maximum-scale=1, minimum-scale=1, user-scalable=no">
    <meta http-equiv="Cache-Control" content="no-siteapp" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
    <meta name="renderer" content="webkit">
    <meta name="apple-mobile-web-app-capable" content="yes" />
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent" />
    <meta name="format-detection" content="telephone=no" />
    <link rel="apple-touch-icon-precomposed" sizes="114x114" href="/apple-touch-icon-114x114-precomposed.png" />
    <meta http-equiv="x-dns-prefetch-control" content="on" />
    <link rel="dns-prefetch" href="http://dns地址" />
    <title></title>
    <meta name="keywords" content="">
    <meta name="description" content="">

<!--
<!DOCTYPE html>
<html lang="zh-cmn-Hans">
<head>
<meta charset="utf-8">
<meta name="viewport" content="initial-scale=1, maximum-scale=1, minimum-scale=1, user-scalable=no">
<meta http-equiv="Cache-Control" content="no-siteapp" />//百度禁止转码
<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />//优先使用 IE 最新版本和 Chrome
<meta name="renderer" content="webkit">//360 使用Google Chrome Frame
<meta name="apple-mobile-web-app-capable" content="yes" /> //是否启用 WebApp 全屏模式
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent" /> //设置状态栏的背景颜色，只有在 `"apple-mobile-web-app-capable" content="yes"` 时生效
<meta name="format-detection" content="telephone=no" /> //禁止数字识自动别为电话号码
<link rel="apple-touch-icon-precomposed" sizes="114x114" href="/apple-touch-icon-114x114-precomposed.png" /> //iOS 图标 :Retina iPhone 和 Retina iTouch，114x114 像素，可以没有，但推荐有
<title>铺铺旺</title>
<meta name="keywords" content="">
<meta name="description" content="">
<meta http-equiv="x-dns-prefetch-control" content="on" /> //用meta信息来告知浏览器, 当前页面要做DNS预解析
<link rel="dns-prefetch" href="http://dns地址" /> //使用link标签来强制对DNS预解析
-->
#### 其他

`placeholder`

`input,button { -webkit-appearance: none; /*去掉苹果的默认UI来渲染按钮*/}`

#### 判断滚动到底部
    $(window).on("scroll",function(){
    	if(($(window).scrollTop() + $(window).height()) >= $("body").height()){
    		loadmpage();
    	}
    	//console.log($(window).scrollTop()+"@@@@"+$(window).height()+"@@@@"+$("#load").offset().top+"@@@"+$("#load").position().top);
    });
