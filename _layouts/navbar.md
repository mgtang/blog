---
layout: default
---
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
<meta name="keywords" content="JS代码,侧边菜单,拉出菜单,高级菜单,导航菜单,jquery菜单" />
<meta name="description" content="jQuery高级可停靠侧边栏，jquery实现的高级侧边导航菜单效果，更多侧边菜单,拉出菜单,高级菜单,导航菜单,jquery菜单请访问柯乐义JS代码频道。" />
<title>jQuery高级可停靠侧边栏_柯乐义</title>
<link type="text/css" rel="Stylesheet" href="http://keleyi.com/keleyi/phtml/jqmenu/2/keleyidock.css" />
<script type="text/javascript" src="http://keleyi.com/keleyi/pmedia/jquery/jquery-1.10.2.min.js"></script>
<script type="text/javascript">
$(document).ready(function () {
var docked = 0;

$("#dock li ul").height($(window).height());

$("#dock .dock-keleyi-com").click(function () {
$(this).parent().parent().addClass("docked").removeClass("free");

docked += 1;
var dockH = ($(window).height()) / docked
var dockT = 0;

$("#dock li ul.docked").each(function () {
$(this).height(dockH).css("top", dockT + "px");
dockT += dockH;
});
$(this).parent().find(".undock").show();
$(this).hide();

if (docked > 0)
$("#content").css("margin-left", "250px");
else
$("#content").css("margin-left", "60px");
});

$("#dock .undock").click(function () {
$(this).parent().parent().addClass("free").removeClass("docked")
.animate({ left: "-180px" }, 200).height($(window).height()).css("top", "0px");

docked = docked - 1;
var dockH = ($(window).height()) / docked
var dockT = 0;

$("#dock li ul.docked").each(function () {
$(this).height(dockH).css("top", dockT + "px");
dockT += dockH;
});
$(this).parent().find(".dock-keleyi-com").show();
$(this).hide();

if (docked > 0)
$("#content").css("margin-left", "250px");
else
$("#content").css("margin-left", "60px");
});

$("#dock li").hover(function () {
$(this).find("ul").animate({ left: "40px" }, 200);
}, function () {
$(this).find("ul.free").animate({ left: "-180px" }, 200);
});
}); 
</script>
</head>
<body>
<ul id="dock">
<li id="links">
<ul class="free">
<li class="header"><a href="#" class="dock-keleyi-com">固定</a><a href="#" class="undock">隐藏</a>链接</li>
<li><a href="http://keleyi.com/menu/cms/" >CMS</a></li><li><a href="http://keleyi.com/menu/net/" >.NET</a></li><li><a href="http://keleyi.com/menu/javascript/" >Javascript</a></li><li><a href="http://keleyi.com/menu/jquery/" >jQuery</a></li><li><a href="http://keleyi.com/menu/csharp/" >C#</a></li><li><a href="http://keleyi.com/menu/aspnet/" >ASP.NET</a></li><li><a href="http://keleyi.com/menu/mvc/" >MVC</a></li><li><a href="http://keleyi.com/menu/html5/" >HTML5</a></li>
<li><a href="http://keleyi.com/menu/webqd/" >web前端</a></li><li><a href="http://keleyi.com/menu/sqlserver/" >SQL Server</a></li><li><a href="http://keleyi.com/menu/cpp/" >C++</a></li><li><a href="http://keleyi.com/menu/hbyy/" >汇编语言</a></li><li><a href="http://keleyi.com/menu/flhz/" >分类汇总</a></li><li><a href="http://keleyi.com/menu/other/" >其他</a></li><li><a href="http://keleyi.com/list/">最新文章</a></li><li><a href="http://keleyi.com/ziliao/js/zzbds.htm">JS正则表达式</a></li>
</ul>
</li>
<li id="files">
<ul class="free">
<li class="header"><a href="#" class="dock-keleyi-com">固定</a><a href="#" class="undock">隐藏</a>游戏</li>
<li><a href="http://keleyi.com/game/1/">HTML5捕鱼游戏</a></li>
<li><a href="http://keleyi.com/game/2/">不上不下</a></li>
<li><a href="http://keleyi.com/game/3/">打地鼠</a></li>
<li><a href="http://keleyi.com/keleyi/phtml/silverlight/">猜数字</a></li>
<li></li>
</ul>
</li>
<li id="tools">
<ul class="free">
<li class="header"><a href="#" class="dock-keleyi-com">固定</a><a href="#" class="undock">隐藏</a>工具</li>
<li><a href="http://keleyi.com/tool/md5.htm">MD5加密</a></li>
<li><a href="http://keleyi.com/tool/htmlencode.htm" target="_blank">HTML编码与解码</a></li>
<li><a href="http://keleyi.com/tool/urldecode.htm" target="_blank">URL编码与解码</a></li>
<li><a href="http://keleyi.com/tool/regex.htm" target="_blank">.NET正则表达式匹配工具</a></li>
<li><a href="http://keleyi.com/ziliao/googlejavascriptstyle.htm">JavaScript代码风格指南</a></li>
<li><a href="http://keleyi.com/ziliao/unicode/">Unicode字符列表</a></li>
<li><a href="http://keleyi.com/tool/color.htm" target="_blank" title="颜色选择器"><img src="http://keleyi.com/tool/color/colormap_80.gif" alt="颜色选择器" /></a></li>
</ul>
</li>
</ul>
