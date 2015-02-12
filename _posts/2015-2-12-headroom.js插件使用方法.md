---
layout: post
title: "headroom.js插件使用方法"
date: 2015-2-12 23:09:04
comments: true
---

1. ##什么是headroom.js？
headroom是用纯Javascript写的插件，用来隐藏和展示页面元素，从而为页面留下更多空间。比如使用headroom能使导航栏当页面下滚时消失，当页面上滚时候又出现。（查看效果）

2. ##工作原理
通过感应目标元素不同的3种状态（原始，下滚，上滚），为目标元素更改相应的class，通过相应的class的css样式的变化得到所要的效果。

3. ##如何使用
（以下的例子是基于bootstrap框架和jquery插件的，在bootstrap框架下可以快速写出导航栏navbar，然后以jquery插件方式对导航栏navbar调用headroom()。）

首先需要引用headroom.js和jQuery.headroom.js。将以下的代码加入到你的代码中。headroom.js作用：感应元素不同的状态为之更改相应的class。jQuery.headroom.js作用：提供jquery插件方式和Data-API方式调用headrooom()。

````
<script  type="text/javascript"  src="https://rawgithub.com/WickyNilliams/headroom.js/master/dist/headroom.js"></script>  
<script  type="text/javascript"  src="https://rawgithub.com/WickyNilliams/headroom.js/master/src/jQuery.headroom.js"></script>  
````


因为headroom()函数传入的参数option对象的默认值如下。

````
{  
    // 在元素没有固定之前，垂直方向的偏移量（以px为单位）  
    offset : 0,  
    // scroll tolerance in px before state changes  
    tolerance : 0,  
    // 对于每个状态都可以自定义css classes   
    classes : {  
        // 当元素初始化后所设置的class  
        initial : "headroom",  
        // 向上滚动时设置的class  
        pinned : "headroom--pinned",  
        // 向下滚动时所设置的class  
        unpinned : "headroom--unpinned"  
    }  
}  
````
由此可知原始的状态对应的class是headroom，下滚时的class是headroom--pinned，上滚时的class是headroom--unpinned。所以我们要添加下面的样式，通过css的trasition属性达到变换效果。

````
<style type="text/css">  
    .headroom {position: fixed;top: 0;left: 0;right: 0;transition: all .2s ease-in-out;}  
    .headroom--unpinned {top: -100px;}  
    .headroom--pinned {top: 0;}  
</style>  
````

之后添加下面的js代码，使用jquery插件的方式调用。".navbar-fixed-top"只是用来获取导航栏navbar，也可以用其他选择器来获取navbar目标元素

````
<script type="text/javascript">  
        $(".navbar-fixed-top").headroom();     
</script>  
````

做完了上述步骤，理论上你就可以看到headroom的效果了，如果没有成功可能是以下的原因：

1. js的引用顺序错误，因为一些js要用到其他js才能运行的，所以必须放在其他的js之后。例如
     <script type="text/javascript">
             $(".navbar-fixed-top").headroom();   
     </script>
必须放在headroom.js和jQuery.headroom.js之后，而headroom.js和jQuery.headroom.js必须放在jQuery.js之后。

2. 将$(".navbar-fixed-top").headroom(); 放在主体html代码之前，如放在<head></head>中，因为在主体html代码之前，navbar元素还没加载就调用了headroom()，所以无效。应该用以下代码替换之，表示等文档加载完毕再调用。
     <script type="text/javascript">`
         $("doucument").ready(fuction(){`
         $(".navbar-fixed-top").headroom(); `
         });  
     </script>`
上述的效果只是通过css自带的trasition属性来实现效果，比较单调。不过可以结合animate.css实现更多的漂亮的消失和出现的效果。（查看效果）

animate.css使用纯css为各种元素实现不同的动画效果，每一种class对应一种动画效果，所以将animate.css引入代码后headroom()可以直接使用已经写好的class。（animate.css下载）

我基于bootstrap和jquery写得例子。

````
<!DOCTYPE html>  
<html>  
  <head>  
    <title>Bootstrap 101 Template</title>  
    <meta name="viewport" content="width=device-width, initial-scale=1.0">  
    <!-- Bootstrap -->  
    <link rel="stylesheet" href="http://cdn.bootcss.com/twitter-bootstrap/3.0.3/css/bootstrap.min.css">  
  
    <link rel="stylesheet" href="I:/webpage/animate/animate.css">  
  
    <!-- HTML5 Shim and Respond.js IE8 support of HTML5 elements and media queries -->  
    <!-- WARNING: Respond.js doesn't work if you view the page via file:// -->  
    <!--[if lt IE 9]>  
        <script src="http://cdn.bootcss.com/html5shiv/3.7.0/html5shiv.min.js"></script>  
        <script src="http://cdn.bootcss.com/respond.js/1.3.0/respond.min.js"></script>  
    <![endif]-->  
    <style type="text/css">  
        .headroom {position: fixed;top: 0;left: 0;right: 0;transition: all .2s ease-in-out;}  
        .headroom--unpinned {top: -100px;}  
        .headroom--pinned {top: 0;}  
    </style>  
  
    <style type="text/css">  
      .scrollspy-example {  
        height: 1200px;  
        overflow: auto;  
        position: relative;  
      }  
    </style>  
  
  
  </head>  
  <body>  
  
    <!-- 页眉大屏显示 -->  
    <div class="jumbotron">  
        <div class="container">  
            <h1>Hello, world!</h1>  
            <p>This is a template for a simple marketing or informational website. It includes a large callout called a jumbotron and three supporting pieces of content. Use it as a starting point to create something more unique.</p>  
            <p><a class="btn btn-primary btn-lg" role="button">Learn more »</a></p>  
        </div>  
    </div>  
  
    <div class="container">  
  
        <!-- 导航栏 -->  
        <nav class="navbar navbar-inverse navbar-fixed-top" role="navigation" id="example">  
            <div class="navbar-header">  
              <a class="navbar-brand" href="#">w3school</a>  
            </div>  
  
            <div class="collapse navbar-collapse" id="tem">  
                <ul class="nav navbar-nav">  
                    <li class="active"><a href="#php">PHP</a></li>  
                    <li><a href="#js">JS</a></li>  
                    <li class="dropdown">  
                        <a href="#" class="dropdown-toggle" data-toggle="dropdown">database<b class="caret"></b></a>  
  
                        <ul class="dropdown-menu">  
                            <li><a href="#mysql">MySQL</a></li>  
                            <li><a href="#pgsql">PostgreSQL</a></li>  
                            <li><a href="#mgdb">MogoDB</a></li>  
                        </ul>  
                    </li>  
                </ul>  
            </div>  
        </nav>  
  
        <!-- 主体内容-->  
        <div data-spy="scroll" data-target="#example" data-offset="0" class="scrollspy-example">  
            <h4 id="php">PHP</h4>  
            <p>PHP, an acronym for Hypertext Preprocessor, is a widely-used open source general-purpose scripting language. It is an HTML embedded scripting language and is especially suited for web development. The basic syntax of PHP is similar to C, Java, and Perl, and is easy to learn. PHP is used for creating interactive and dynamic web pages quickly, but you can do much more with PHP.  
             </p>  
            <h4 id="js">JS</h4>  
            <p>  
            JavaScript is a cross-platform, object-oriented scripting language developed by Netscape. JavaScript was created by Netscape programmer Brendan Eich. It was first released under the name of LiveScript as part of Netscape Navigator 2.0 in September 1995. It was renamed JavaScript on December 4, 1995. As JavaScript works on the client side, It is mostly used for client-side web development.  
            </p>  
            <h4 id="mysql">MySQL</h4>  
            <p>  
            MySQL tutorial of w3cschool is a comprhensive tutorial to learn MySQL. We have hundreds of examples covered, often with PHP code. This helps you to learn how to create PHP-MySQL based web applications.  
            </p>  
            <h4 id="pgsql">PostgreSQL</h4>  
            <p>  
            In 1986 the Defense Advanced Research Projects Agency (DARPA), the Army Research Office (ARO), the National Science Foundation (NSF), and ESL, Inc sponsored Berkeley POSTGRES Project which was led by Michael Stonebrakessr. In 1987 the first demo version of the project is released. In June 1989, Version 1 was released to some external users. Version 2 and 3 were released in 1990 and 1991. Version 3 had support for multiple storage managers, an query executor was improved, rule system was rewritten. After that, POSTGRES has been started to be implemented in various research and development projects. For example, in late 1992, POSTGRES became the primary data manager for the Sequoia 2000 scientific computing project4. User community around the project also has been started increasing; by 1993, it was doubled.  
            </p>  
            <h4 id="mgdb">MongoDB</h4>  
            <p>  
            The term NoSQL was coined by Carlo Strozzi in the year 1998. He used this term to name his Open Source, Light Weight, DataBase which did not have an SQL interface.In the early 2009, when last.fm wanted to organize an event on open-source distributed databases, Eric Evans, a Rackspace employee, reused the term to refer databases which are non-relational, distributed, and does not conform to atomicity, consistency, isolation, durability - four obvious features of traditional relational database systems.  
            </p>  
            <p>  
            After reading the largest third party online MySQL tutorial by w3cschool, you will be able to install, manage and develop PHP-MySQL web applications by your own. We have a comprehensive, SQL TUTORIAL, which will help you to understand how to prepare queries to fetch data against various conditions.  
            </p>  
  
        </div>  
    </div>  
  
  
    <!-- jQuery (necessary for Bootstrap's JavaScript plugins) -->  
    <script src="http://cdn.bootcss.com/jquery/1.10.2/jquery.min.js"></script>  
    <!-- Include all compiled plugins (below), or include individual files as needed -->  
    <script src="http://cdn.bootcss.com/twitter-bootstrap/3.0.3/js/bootstrap.min.js"></script>  
  
  
    <script  type="text/javascript"  src="https://rawgithub.com/WickyNilliams/headroom.js/master/dist/headroom.js"></script>  
  
    <script  type="text/javascript"  src="https://rawgithub.com/WickyNilliams/headroom.js/master/src/jQuery.headroom.js"></script>  
  
    <script type="text/javascript">  
  
            $(".navbar-fixed-top").headroom();  
  
    </script>  
  
  
  </body>  
</html>  
````
