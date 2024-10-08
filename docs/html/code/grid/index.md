# 🍁Grid九宫格

::: tip 说明

本站专注于收集前端相关资源，持续更新！！！

如果这些资源对你有帮助，可以给一个 star 支持下 [前端-资源库](https://github.com/huangpw/document-frontend-vitepress) ，如果您发现有 【 **[HTML](/html) 、[Vue](/vue) 、[React](/react) 、[Angular](/angular) 、[Electron](/electron)** 】 等优秀的开源项目。请 [点此推荐](https://github.com/huangpw/document-frontend-vitepress/issues/new) 。

:::

## HTML5九宫格布局

![img](/images/html/code/grid/10001.png)

```html
<!DOCTYPE html>
<html>
<head>
<title>html5响应式九宫格</title>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<meta name="viewport" content="width=device-width,height=device-height,inital-scale=1.0,maximum-scale=1.0,user-scalable=no;" />
<meta name="apple-mobile-web-app-capable" content="yes" />
<meta name="apple-mobile-web-app-status-bar-style" content="black" />
<meta name="format-detection" content="telephone=no" />
<meta charset="utf-8" />
<style type="text/css">
    html, body { color:#222; font-family:Microsoft YaHei, Helvitica, Verdana, Tohoma, Arial, san-serif; margin:0; padding: 0; text-decoration: none; }
    img { border:0; }
    ul { list-style: none outside none; margin:0; padding: 0; }
    body {
        background-color:#eee;
    }
    body .mainmenu:after { clear: both; content: " "; display: block; }

    body .mainmenu li{
        float:left;
        margin-left: 2.5%;
        margin-top: 2.5%;
        width: 30%; 
        border-radius:3px;
        overflow:hidden;
    }

    body .mainmenu li a{ display:block;  color:#FFF;   text-align:center }
    body .mainmenu li a b{
        display:block; height:80px;
    }
    body .mainmenu li a img{
        margin: 15px auto 15px;
        width: 50px;
        height: 50px;
    }

    body .mainmenu li a span{ display:block; height:30px; line-height:30px;background-color:#FFF; color: #999; font-size:14px; }

    body .mainmenu li:nth-child(8n+1) {background-color:#36A1DB}
    body .mainmenu li:nth-child(8n+2) {background-color:#678ce1}
    body .mainmenu li:nth-child(8n+3) {background-color:#8c67df}
    body .mainmenu li:nth-child(8n+4) {background-color:#84d018}
    body .mainmenu li:nth-child(8n+5) {background-color:#14c760}
    body .mainmenu li:nth-child(8n+6) {background-color:#f3b613}
    body .mainmenu li:nth-child(8n+7) {background-color:#ff8a4a}
    body .mainmenu li:nth-child(8n+8) {background-color:#fc5366}
</style>
</head>

<body>
    <ul class="mainmenu">
        <li><a href="/" ><b><img src="images/tb01.png" /></b><span>关于我们</span></a></li>
        <li><a href="/" ><b><img src="images/tb02.png" /></b><span>新闻中心</span></a></li>
        <li><a href="/" ><b><img src="images/tb03.png" /></b><span>产品展示</span></a></li>
        <li><a href="/" ><b><img src="images/tb04.png" /></b><span>成功案例</span></a></li>
        <li><a href="/" ><b><img src="images/tb05.png" /></b><span>下载中心</span></a></li>
        <li><a href="/" ><b><img src="images/tb06.png" /></b><span>团队介绍</span></a></li>
        <li><a href="/" ><b><img src="images/tb06.png" /></b><span>人才招聘</span></a></li>
        <li><a href="/" ><b><img src="images/tb07.png" /></b><span>联系我们</span></a></li>
        <li><a href="/" ><b><img src="images/tb08.png" /></b><span>在线留言</span></a></li>         
    </ul>
</body>
</html>
```

