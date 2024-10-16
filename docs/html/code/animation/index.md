# 🍁Animation动画

::: tip 说明

本站专注于收集前端相关资源，持续更新！！！

如果这些资源对你有帮助，可以给一个 star 支持下 [前端-资源库](https://github.com/huangpw/document-frontend-vitepress) ，如果您发现有 【 **[HTML](/html) 、[Vue](/vue) 、[React](/react) 、[Angular](/angular) 、[Electron](/electron)** 】 等优秀的开源项目。请 [点此推荐](https://github.com/huangpw/document-frontend-vitepress/issues/new) 。

:::



## 1. 鼠标悬浮文字阴影跳动

效果图

![img](https://segmentfault.com/img/bVc4uog)

代码

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        h1 {
            width: 80px;
            color: cornflowerblue;
        }

        h1:hover {
            animation: animate 0.5s linear infinite;
        }

        @keyframes animate {

            0%,
            25% {
                text-shadow: 2px 2px 2px #ff6384;
            }

            50% {
                text-shadow: 2px -2px 2px #ff6384;
            }

            75% {
                text-shadow: -2px 2px 2px #ff6384;
            }

            100% {
                text-shadow: -2px -2px 2px #ff6384;
            }
        }
    </style>
</head>

<body>
    <h1>hello</h1>
    <!-- 
        一说到阴影，我们常常就会想到盒子的阴影，box-shadow。实际上css3另外提供了文字阴影text-shadow
        text-shadow对应属性 text-shadow: h-shadow v-shadow blur color;
                                         水平阴影 垂直阴影 模糊范围 颜色值
        本例中，当鼠标悬浮的时候，给文字加上动画。四个方向依次都出现文字阴影，就类似跳动的效果了
    -->
</body>

</html>
```

## 2.鼠标悬浮文字底部出现下划线并变宽

效果图

![img](https://segmentfault.com/img/bVc4uol)

代码

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .box {
            width: 160px;
            /* 外盒子相对定位，便于伪元素绝对定位(使下划线在文字的最底下) */
            position: relative;
        }

        h1::before {
            content: '';
            height: 4px;
            background: red;
            /* 伪元素默认样式 display: inline;所以需要转成inline-block宽高才会生效 */
            display: inline-block;
            /* 通过定位使下划线在最低层 */
            position: absolute;
            bottom: -6px;
            width: 0;
            /* 加上一个过渡效果，使之丝滑一些 */
            transition: width 0.36s;
        }

        h1:hover::before {
            /* 悬浮时候，让下划线伪元素宽度变成100%即可出现效果 */
            width: 100%;
        }
    </style>
</head>

<body>
    <div class="box">
        <h1>悬浮下划线</h1>
    </div>
    <!-- 
        思路：
            1. 使用伪元素创建下划线
            2. 通过定位让下划线的位置在文字的底部
            3. 初始下划线宽度为0
            4. 悬浮时更改为100%即出现效果
     -->
</body>

</html>
```

## 3. 文字颜色渐变流光效果

效果图

![img](https://segmentfault.com/img/bVc4uon)

代码

```html
<!DOCTYPE html>
<html>

<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
        /* 加上 -webkit- 注意兼容 */
        h1 {
            background: -webkit-linear-gradient(135deg,
                    #0eaf6d,
                    #ff6ac6 25%,
                    #147b96 50%,
                    #e6d205 55%,
                    #2cc4e0 60%,
                    #8b2ce0 80%,
                    #ff6384 95%,
                    #08dfb4);
            /* 文字颜色填充设置为透明 */
            -webkit-text-fill-color: transparent;
            /* 背景裁剪，即让文字使用背景色 */
            -webkit-background-clip: text;
            /* 背景图放大一下，看着柔和一些 */
            -webkit-background-size: 200% 100%;
            /* 应用动画flowCss 12秒速度 无限循环 线性匀速动画*/
            -webkit-animation: flowCss 12s infinite linear;
        }

        @-webkit-keyframes flowCss {
            0% {
                /* 移动背景位置 */
                background-position: 0 0;
            }

            100% {
                background-position: -400% 0;
            }
        }

        h1:hover {
            -webkit-animation: flowCss 4s infinite linear;
        }
    </style>
</head>

<body>
    <h1>文字颜色渐变流光效果</h1>
    <!-- 思路就是 文字颜色填充为透明、背景裁剪让文字使用背景色、然后设置一个渐变背景色
    再放大一下背景，最后通过动画移动背景位置，于是效果就出来了 -->
</body>

</html>
```

## 4. 打字机效果

效果图

![img](https://segmentfault.com/img/bVc4uop)

代码

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        h1 {
            /* 本例12个文字(加标点符号)；有多少个文字，width就是多少个em */
            width: 12em;
            /* 加上两个动画，一个是打字动画，使用steps让字一个一个的出现，
             注意step和字数保持一致，光标动画也是同理，*/
            animation: typingWords 5s steps(12) infinite, cursor 0.5s steps(1) infinite;
            /* 要设置不允许换行，且溢出隐藏 */
            white-space: nowrap;
            overflow: hidden;
            /* 使用右边框作为打印的指针光标 */
            border-right: 1px solid #000;
        }

        @keyframes typingWords {
            0% {
                width: 0;
            }
        }

        @keyframes cursor {
            50% {
                border-color: transparent;
            }
        }
    </style>
</head>

<body>
    <h1>欢迎光临呐，各位访客们。</h1>
    <!-- css大佬张鑫旭的实现方式：https://www.zhangxinxu.com/wordpress/2019/01/css-typewriter-effect/ -->
</body>

</html>
```

## 4. 文字左右旋转晃动效果

效果图

![img](https://segmentfault.com/img/bVc4uoq)

代码

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        span {
            font-size: 48px;
            font-weight: 600;
            animation: rotate 0.3s ease infinite;
            /* 注意，要开启绝对定位哦 */
            position: absolute;
        }

        /* 鼠标悬浮开启动画也可以的
        span:hover {
            animation: rotate 0.3s ease infinite;
        } */

        @keyframes rotate {
            0% {
                transform: rotate(0);
            }

            20% {
                transform: rotate(-2deg);
            }

            60% {
                transform: rotate(0);
            }

            80% {
                transform: rotate(2deg);
            }

            100% {
                transform: rotate(0);
            }
        }

        span:nth-child(2) {
            margin-left: 108px;
        }

        span:nth-child(3) {
            margin-left: 216px;
        }
    </style>
</head>

<body>
    <span>代码</span>
    <span>修仙</span>
    <span>之路</span>
</body>

</html>
```

## 5. 圆圈呼吸扩散效果

效果图

![img](https://segmentfault.com/img/bVc4uor)

代码

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        body {
            margin: 120px;
        }

        .circle-breath {
            background: pink;
            box-shadow: 0 0 0 0 rgb(204, 73, 152);
            height: 36px;
            width: 36px;
            border-radius: 50%;
            animation: donghua 2.4s infinite;
        }

        @keyframes donghua {
            0% {
                transform: scale(0.60);
                /* 注意rgba中的a的设置 */
                box-shadow: 0 0 0 0 rgba(204, 73, 152, 60%);
            }

            60% {
                transform: scale(1);
                box-shadow: 0 0 0 36px rgba(204, 73, 152, 0%);
            }

            100% {
                transform: scale(0.60);
                box-shadow: 0 0 0 0 rgba(204, 73, 152, 0%);
            }
        }
    </style>
</head>

<body>
    <div class="circle-breath"></div>
    <!-- 
        动画中应用背景色阴影，背景色阴影初始透明度为60%，后续为0
        搭配使用scale进行缩放，便可以达到圆圈呼吸扩散效果
     -->
</body>

</html>
```

## 6. 四周线条环绕流动效果

效果图

![img](https://segmentfault.com/img/bVc4uoC)

代码

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        body {
            padding: 120px;
        }

        .mainbox {
            width: 320px;
            height: 320px;
            position: relative;
            /* 超出隐藏需要加上 */
            overflow: hidden;
        }

        .content {
            width: 320px;
            height: 320px;
            line-height: 320px;
            text-align: center;
            background-color: #cde;
        }

        .line {
            /* 结合外层元素的相对定位 */
            position: absolute;
        }

        .line:nth-child(1) {
            top: 0;
            left: 0;
            width: 100%;
            height: 3px;
            /* 加上渐变效果，方可形成拖尾效果 */
            background: linear-gradient(90deg, transparent, orange);
            animation: animate1 8s linear infinite;
        }

        /* 分别控制其上下左右的定位距离，从而形成线条跟随效果 */
        @keyframes animate1 {
            0% {
                left: -100%;
            }

            50%,
            100% {
                left: 100%;
            }
        }

        .line:nth-child(2) {
            top: -100%;
            right: 0;
            width: 3px;
            height: 100%;
            background: linear-gradient(180deg, transparent, red);
            animation: animate2 8s linear infinite;
            /* 注意要加上延时触发动画效果，这样线条才会依次触发 */
            animation-delay: 2s;
        }

        @keyframes animate2 {
            0% {
                top: -100%;
            }

            50%,
            100% {
                top: 100%;
            }
        }

        .line:nth-child(3) {
            bottom: 0;
            right: 0;
            width: 100%;
            background: linear-gradient(270deg, transparent, green);
            animation: animate3 8s linear infinite;
            animation-delay: 4s;
        }

        @keyframes animate3 {
            0% {
                right: -100%;
                height: 3px;
            }

            50%,
            100% {
                height: 2px;
                right: 100%;
            }
        }

        .line:nth-child(4) {
            bottom: -100%;
            left: 0;
            width: 3px;
            height: 100%;
            background: linear-gradient(360deg, transparent, #3a86ff);
            animation: animate4 8s linear infinite;
            animation-delay: 6s;
        }

        @keyframes animate4 {
            0% {
                bottom: -100%;
            }

            50%,
            100% {
                bottom: 100%;
            }
        }
    </style>
</head>

<body>
    <div class="mainbox">
        <span class="line"></span>
        <span class="line"></span>
        <span class="line"></span>
        <span class="line"></span>
        <div class="content">线条环绕</div>
    </div>
</body>

</html>
```

## 7. 鼠标悬浮开门关门效果

效果图

![img](https://segmentfault.com/img/bVc4sAP)

代码

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        body {
            box-sizing: border-box;
            padding: 160px 0 0 240px;
        }

        /* 门容器样式 */
        .doorWrap {
            width: 320px;
            height: 320px;
            border: 1px solid #666;
            perspective: 500px;
            position: relative;
            display: flex;
        }

        /* 左门右门的共有样式 */
        .leftDoor,
        .rightDoor {
            width: 50%;
            height: 100%;
            background-color: rgb(194, 37, 37);
            transition: 1.2s;
            z-index: 2;
            display: flex;
            justify-content: center;
            align-items: center;
            border: 1px solid #333;
        }

        /* 设置旋转元素的基点，左边大门以左侧为基准点旋转 */
        .leftDoor {
            transform-origin: left;
        }

        /* 设置旋转元素的基点，右边大门以右侧为基准点旋转 */
        .rightDoor {
            transform-origin: right;
        }

        /* 当鼠标悬浮的时候，设置开门的幅度，左门往左侧开 */
        .doorWrap:hover .leftDoor {
            transform: rotateY(-130deg);
        }

        /* 右门往右侧开 */
        .doorWrap:hover .rightDoor {
            transform: rotateY(130deg);
        }

        /* 内容区的定位层级稍微低一些 */
        .content {
            position: absolute;
            z-index: 1;
            width: 100%;
            height: 100%;
            background-color: #abf;
            display: flex;
            justify-content: center;
            align-items: center;
        }
    </style>
</head>

<body>
    <div class="doorWrap">
        <div class="leftDoor">左门</div>
        <div class="rightDoor">右门</div>
        <div class="content">欢迎光临，客官里边请...</div>
    </div>
</body>

</html>
```

## 8.背景颜色流动效果

效果图

![img](https://segmentfault.com/img/bVc4upx)

代码

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .bg {
            margin: 60px;
            width: 32%;
            height: 48vh;
            background: linear-gradient(-45deg, #dae, #f66, #3c9, #09f, #66f);
            background-size: 200% 200%;
            animation: gradient 8s ease infinite;
        }

        @keyframes gradient {
            0% {
                background-position: 0 12%;
            }

            50% {
                background-position: 100% 100%;
            }

            100% {
                background-position: 0 12%;
            }
        }
    </style>
</head>

<body>
    <div class="bg"></div>
</body>

</html>
```



## 9.钟摆效果

效果图

![img](https://segmentfault.com/img/bVc4upI)

代码

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        /* 画一条钟摆线条 */
        .line {
            margin: 24px 0 0 320px;
            width: 6px;
            height: 320px;
            background: #baf;
            border-radius: 8px;
            /* 钟摆动画周期两秒、匀速运动、无限循环 */
            animation: pendulum 3s linear infinite;
            /* 旋转以上方中间为中心进行旋转，因为默认是中间中心旋转 */
            transform-origin: top;
            /* 注意因为钟摆的小球是使用伪元素画的，故这里要加上定位 */
            position: relative;
        }

        /* 使用伪元素画钟摆小球，这样在旋转的时候，小球就一致跟着钟摆线了 */
        .line::after {
            content: '';
            width: 32px;
            height: 32px;
            border-radius: 50%;
            background-color: #faa;
            /* 伪元素搭配定位方便调整小球的位置 */
            position: absolute;
            bottom: 0;
            left: -12px;
        }

        /* 钟摆动画rotate旋转起来 */
        @keyframes pendulum {
            0% {
                transform: rotate(0deg);
            }

            25% {
                transform: rotate(45deg);
            }

            50% {
                transform: rotate(0deg);
            }

            75% {
                transform: rotate(-45deg);
            }

            100% {
                transform: rotate(0deg);
            }
        }
    </style>
</head>

<body>
    <div class="line"></div>
</body>

</html>
```

## 10.文字烟雾消散效果

效果图

![img](https://segmentfault.com/img/bVc4upQ)

代码

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        /* 主要是text-shadow和transform搭配动画的巧妙运用 */
        .wrap {
            width: 600px;
            height: 480px;
            box-sizing: border-box;
            padding: 120px;
            background-color: #000;
            color: transparent;
            display: flex;
        }

        h3 {
            text-shadow: 0 0 0 #fff;
            animation: smoky 6s infinite;
        }

        @keyframes smoky {
            60% {
                text-shadow: 0 0 40px #fff;
            }

            100% {
                text-shadow: 0 0 20px #fff;
                /* 这里是重点 */
                transform: translate3d(15rem, -8rem, 0) rotate(-40deg) skew(70deg) scale(1.5);
                opacity: 0;
            }
        }

        h3:nth-child(1) {
            animation-delay: 1s;
        }

        h3:nth-child(2) {
            animation-delay: 1.4s;
        }

        h3:nth-child(3) {
            animation-delay: 1.8s;
        }

        h3:nth-child(4) {
            animation-delay: 2.2s;
        }

        h3:nth-child(5) {
            animation-delay: 2.6s;
        }
    </style>
</head>

<body>
    <div class="wrap">
        <h3>代码</h3>
        <h3>修仙</h3>
        <h3>之路</h3>
        <h3>道阻</h3>
        <h3>且长...</h3>
    </div>
</body>

</html>
```

## 11.水平左右抖动效果

效果图

![img](https://segmentfault.com/img/bVc4upS)

代码

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        body {
            box-sizing: border-box;
            padding: 120px;
        }

        .target {
            width: 48px;
            height: 48px;
            line-height: 48px;
            text-align: center;
            font-weight: bold;
            color: red;
            background: #baf;
            transform-origin: bottom;
            animation: shaking 1.2s ease-in-out infinite;
            /* 初始暂停播放，后续通过js控制播放 */
            animation-play-state: paused;
        }

        /* 通过translate3d的x轴移动去控制水平移动抖动效果 */
        @keyframes shaking {

            10%,
            90% {
                transform: translate3d(-1.2px, 0, 0);
            }

            20%,
            80% {
                transform: translate3d(2px, 0, 0);
            }

            30%,
            70% {
                transform: translate3d(-4.8px, 0, 0);
            }

            40%,
            60% {
                transform: translate3d(4.8px, 0, 0);
            }

            50% {
                transform: translate3d(-4.8px, 0, 0);
            }
        }
    </style>
</head>

<body>
    <div class="target">^_^</div>
    <br>
    <button class="start">动画开始</button>
    <button class="pause">动画暂停</button>
    <script>
        // js去设置animationPlayState属性值从而控制动画播放
        let startBtn = document.querySelector('.start')
        let pauseBtn = document.querySelector('.pause')
        let target = document.querySelector('.target')
        startBtn.onclick = () => {
            target.style.animationPlayState = 'running'
        }
        pauseBtn.onclick = () => {
            target.style.animationPlayState = 'paused'
        }
    </script>
</body>

</html>
```

## 12.垂直方向坠落弹跳效果

效果图

![img](https://segmentfault.com/img/bVc4upT)

代码

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        body {
            box-sizing: border-box;
            padding: 120px;
        }

        .target {
            background: #666;
            width: 108px;
            height: 60px;
            border-radius: 60px;
            color: aliceblue;
            font-weight: bolder;
            line-height: 60px;
            text-align: center;
        }

        .animationClass {
            animation: 1.2s ease 0s infinite backwards bounce;
        }


        /* 主要是通过控制translateY的值来操作y轴的距离实现弹跳效果 */
        @keyframes bounce {
            0% {
                transform: translateY(-64px);
                animation-timing-function: ease-in;
                opacity: 1;
            }

            24% {
                opacity: 1;
            }

            40% {
                transform: translateY(-32px);
                animation-timing-function: ease-in;
            }

            62% {
                transform: translateY(-16px);
                animation-timing-function: ease-in;
            }

            82% {
                transform: translateY(-8px);
                animation-timing-function: ease-in;
            }

            92% {
                transform: translateY(-4px);
                animation-timing-function: ease-in;
            }

            25%,
            55%,
            75%,
            90% {
                transform: translateY(0);
                animation-timing-function: ease-out;
            }

            100% {
                transform: translateY(0);
                animation-timing-function: ease-out;
                opacity: 1;
            }
        }
    </style>
</head>

<body>
    <div class="target">O__O</div>
    <br>
    <button class="start">动画开始</button>
    <button class="end">动画结束</button>
    <script>
        let startBtn = document.querySelector('.start')
        let endBtn = document.querySelector('.end')
        let targetBox = document.querySelector('.target')
        // 通过dom的classList的API去控制动画的开始和结束(添加类移除类)
        startBtn.onclick = () => {
            targetBox.classList.add('animationClass')
        }
        endBtn.onclick = () => {
            targetBox.classList.remove('animationClass')
        }
    </script>
</body>

</html>
```

## 13.文字横向伸展模糊淡入淡出效果

效果图

![img](https://segmentfault.com/img/bVc4uqb)

代码

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .enter {
            margin-top: 120px;
            text-align: center;
            /* 贝塞尔曲线动画 */
            animation: enterenter 1.8s infinite cubic-bezier(0.250, 0.460, 0.450, 0.940) both;
        }

        @keyframes enterenter {
            0% {
                /* 加上文字间距 */
                letter-spacing: 1em;
                /* Z轴变换 */
                transform: translateZ(300px);
                /* filter: blur(); 像素模糊效果 */
                filter: blur(12px);
                /* 透明度也要改变 */
                opacity: 0;
            }

            100% {
                transform: translateZ(12px);
                filter: blur(0);
                opacity: 1;
            }
        }

        .leave {
            text-align: center;
            animation: leaveleave 1.8s infinite cubic-bezier(0.250, 0.460, 0.450, 0.940) both;
        }

        @keyframes leaveleave {
            0% {
                transform: translateZ(0);
                filter: blur(0.01);
            }

            100% {
                letter-spacing: 1em;
                transform: translateZ(300px);
                filter: blur(12px) opacity(0%);
            }
        }
    </style>
</head>

<body>
    <h2 class="enter">早上好，程序猿兽们</h2>
    <br>
    <h2 class="leave">晚上好，程序猿兽们</h2>
</body>

</html>
```

## 14.四个方向盒子旋转移动进入效果

效果图

![img](https://segmentfault.com/img/bVc4uqf)

代码

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        body {
            overflow: hidden;
        }

        .target1 {
            width: 72px;
            height: 72px;
            background-color: #baf;
            /* 左侧滚动旋转进入 */
            animation: leftEnter 1.5s infinite ease-out both;
            position: absolute;
            left: 45%;
            top: 30%;
        }

        @keyframes leftEnter {
            0% {
                transform: translateX(-1000px) rotate(-540deg);
                opacity: 0;
            }

            100% {
                transform: translateX(0) rotate(0deg);
                opacity: 1;
            }
        }

        .target2 {
            width: 72px;
            height: 72px;
            background-color: #abf;
            /* 右侧滚动旋转进入 */
            animation: rightEnter 1.5s infinite ease-out both;
            position: absolute;
            left: 45%;
            top: 40%;
        }

        @keyframes rightEnter {
            0% {
                transform: translateX(1000px) rotate(540deg);
                opacity: 0;
            }

            100% {
                transform: translateX(0) rotate(0deg);
                opacity: 1;
            }
        }

        .target3 {
            width: 72px;
            height: 72px;
            background-color: pink;
            /* 上方滚动旋转进入 */
            animation: topEnter 1.5s infinite ease-out both;
            position: absolute;
            left: 45%;
            top: 50%;
        }

        @keyframes topEnter {
            0% {
                transform: translateY(-800px) rotate(540deg);
                opacity: 0;
            }

            100% {
                transform: translateX(0) rotate(0deg);
                opacity: 1;
            }
        }

        .target4 {
            width: 72px;
            height: 72px;
            background-color: rgb(211, 140, 233);
            /* 下方滚动旋转进入 */
            animation: bottomEnter 1.5s infinite ease-out both;
            position: absolute;
            left: 45%;
            top: 20%;
        }

        @keyframes bottomEnter {
            0% {
                transform: translateY(1200px) rotate(540deg);
                opacity: 0;
            }

            100% {
                transform: translateX(0) rotate(0deg);
                opacity: 1;
            }
        }
    </style>
</head>

<body>
    <div class="target1"></div>
    <div class="target2"></div>
    <div class="target3"></div>
    <div class="target4"></div>
</body>

</html>
```

## 15.按钮点击波纹效果

效果图

![img](https://segmentfault.com/img/bVc4uqg)

代码

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        body {
            padding: 120px;
            background-color: #999;
        }

        button {
            margin: 8px;
            width: 120px;
            height: 48px;
            background-color: #faa;
            color: #fff;
            border: none;
            border-radius: 12px;
            cursor: pointer;
            /* 开启定位是为了给波纹动画元素使用 */
            position: relative;
            /* 必须加上超出隐藏，注释掉以后效果很明显 */
            overflow: hidden;
            /* hover过渡一下 */
            transition: all 0.3s;
        }

        button:hover {
            box-shadow: 0 0 18px rgba(255, 255, 255, 0.36);
        }

        .btn2 {
            background-color: violet;
        }

        .btn3 {
            background-color: rgb(231, 116, 164);
        }

        .btn4 {
            background-color: rgb(116, 204, 231);
        }

        .btn5 {
            background-color: rgb(54, 134, 58);
        }

        .btn6 {
            background-color: rgb(224, 126, 45);
        }

        .ripple {
            position: absolute;
            border-radius: 50%;
            background-color: rgba(255, 255, 255, 0.48);
            transform: scale(0);
            animation: ripple 240ms linear;
        }

        @keyframes ripple {
            to {
                transform: scale(2.4);
                opacity: 0.12;
            }
        }
    </style>
</head>

<body>
    <button class="targetBtn">点击波纹效果</button>
    <button class="targetBtn btn2">点击波纹效果</button>
    <button class="targetBtn btn3">点击波纹效果</button>
    <button class="targetBtn btn4">点击波纹效果</button>
    <button class="targetBtn btn5">点击波纹效果</button>
    <button class="targetBtn btn6">点击波纹效果</button>
    <script>
        // 创建波纹函数，只要一点击就创建一个波纹
        function createRipple(event) {
            const button = event.target; // 获取事件对象button按钮
            const circle = document.createElement("div"); // 创建一个div标签用于表示一个波纹（波纹就是一个圆）
            const diameter = Math.max(button.clientWidth, button.clientHeight); // 取dom宽度和高度中的一个最大值，以最大值做直径
            const radius = diameter / 2; // 直径除以2即为半径 （若不理解这几行，可注释掉overflow: hidden;再点击按钮即明白）
            circle.style.width = circle.style.height = `${diameter}px`; // 以直径作为宽高
            circle.style.left = `${event.clientX - button.offsetLeft - radius}px`; // 设置定位的位置
            circle.style.top = `${event.clientY - button.offsetTop - radius}px`;
            circle.classList.add("ripple"); // classList加上类名既有动画效果了
            // 若有这个波纹动画圆dom以后，就移除这个dom再追加。若没有直接追加
            let ripple = button.querySelector('.ripple')
            if (ripple) {
                ripple.remove();
            }
            button.appendChild(circle); // 将这个波纹动画圆作为子元素追加到父元素button上（这样父元素相对定位，子元素绝对定位就生效了）
        }
        // 1. 获取将要点击的按钮dom数组
        const targetBtnArr = document.querySelectorAll('.targetBtn')
        // 2. 给数组中的每一项，即要点击的按钮dom绑定点击监听事件
        for (let i = 0; i < targetBtnArr.length; i++) {
            let targetBtn = targetBtnArr[i]
            targetBtn.addEventListener("click", createRipple);
        }
    </script>
</body>


</html>
```

## 16.鼠标悬浮按钮边框线条动画效果

效果图

![img](https://segmentfault.com/img/bVc4uqi)

代码

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        body {
            background: #faa;
            padding: 120px;
        }

        button {
            display: inline-block;
            border: none;
            color: #fff;
            cursor: pointer;
            margin: 12px 18px;
            background: rgb(201, 108, 234);
            position: relative;
        }

        span {
            display: block;
            padding: 18px 60px
        }

        button::before,
        button::after {
            content: "";
            width: 0;
            height: 2px;
            position: absolute;
            transition: all .2s linear;
            background: #fff
        }

        span::before,
        span::after {
            content: "";
            width: 2px;
            height: 0;
            position: absolute;
            transition: all .2s linear;
            background: #fff
        }

        button:hover::before,
        button:hover::after {
            width: 100%
        }

        button:hover span::before,
        button:hover span::after {
            height: 100%
        }

        .btn1::before,
        .btn1::after {
            transition-delay: .2s
        }

        .btn1 span::before,
        .btn1 span::after {
            transition-delay: 0s
        }

        .btn1::before {
            right: 0;
            top: 0
        }

        .btn1::after {
            left: 0;
            bottom: 0
        }

        .btn1 span::before {
            left: 0;
            top: 0
        }

        .btn1 span::after {
            right: 0;
            bottom: 0
        }

        .btn1:hover::before,
        .btn1:hover::after {
            transition-delay: 0s
        }

        .btn1:hover span::before,
        .btn1:hover span::after {
            transition-delay: .2s
        }

        .btn2::before,
        .btn2::after {
            transition-delay: 0s
        }

        .btn2 span::before,
        .btn2 span::after {
            transition-delay: .2s
        }

        .btn2::before {
            right: 0;
            top: 0
        }

        .btn2::after {
            left: 0;
            bottom: 0
        }

        .btn2 span::before {
            left: 0;
            top: 0
        }

        .btn2 span::after {
            right: 0;
            bottom: 0
        }

        .btn2:hover::before,
        .btn2:hover::after {
            transition-delay: .2s
        }

        .btn2:hover span::before,
        .btn2:hover span::after {
            transition-delay: 0s
        }

        .btn3::after {
            left: 0;
            bottom: 0;
            transition-delay: .6s
        }

        .btn3 span::after {
            transition-delay: .4s;
            right: 0;
            bottom: 0
        }

        .btn3::before {
            right: 0;
            top: 0;
            transition-delay: .2s
        }

        .btn3 span::before {
            transition-delay: 0s;
            left: 0;
            top: 0
        }

        .btn3:hover::after {
            transition-delay: 0s
        }

        .btn3:hover span::after {
            transition-delay: .2s
        }

        .btn3:hover::before {
            transition-delay: .4s
        }

        .btn3:hover span::before {
            transition-delay: .6s
        }

        .btn4::after {
            right: 0;
            bottom: 0;
            transition-duration: .4s
        }

        .btn4 span::after {
            right: 0;
            bottom: 0;
            transition-duration: .4s
        }

        .btn4::before {
            left: 0;
            top: 0;
            transition-duration: .4s
        }

        .btn4 span::before {
            left: 0;
            top: 0;
            transition-duration: .4s
        }

        .btn5::after {
            left: 0;
            bottom: 0;
            transition-duration: .4s
        }

        .btn5 span::after {
            right: 0;
            top: 0;
            transition-duration: .4s
        }

        .btn5::before {
            right: 0;
            top: 0;
            transition-duration: .4s
        }

        .btn5 span::before {
            left: 0;
            bottom: 0;
            transition-duration: .4s
        }

        .btn6::before {
            left: 50%;
            top: 0;
            transition-duration: .4s
        }

        .btn6::after {
            left: 50%;
            bottom: 0;
            transition-duration: .4s
        }

        .btn6 span::before {
            left: 0;
            top: 50%;
            transition-duration: .4s
        }

        .btn6 span::after {
            right: 0;
            top: 50%;
            transition-duration: .4s
        }

        .btn6:hover::before,
        .btn6:hover::after {
            left: 0
        }

        .btn6:hover span::before,
        .btn6:hover span::after {
            top: 0
        }
    </style>
</head>

<body>
    <main>
        <button class="btn1"><span>悬浮上左、下右</span></button>
        <button class="btn2"><span>悬浮右上、左下</span></button>
        <button class="btn3"><span>悬浮之一圈线条</span></button>
        <button class="btn4"><span>悬浮右下角和左上角两个方向延伸</span></button>
        <button class="btn5"><span>悬浮右上角和左下角两个方向延伸</span></button>
        <button class="btn6"><span>悬浮四个方向中间点往两端延伸</span></button>
    </main>
</body>

</html>
```

## 17.灯泡开关效果

效果图

![img](https://segmentfault.com/img/bVc4uqj)

代码

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        /* :root全局css变量搭配var()函数使用 */
        :root {
            --light-color: #fff
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            width: 100%;
            height: 100vh;
        }

        .container {
            width: 100%;
            height: 100%;
            display: flex;
        }

        .light-container {
            width: 100%;
            display: flex;
            justify-content: center;
            align-items: center;
            background-color: #333;
        }

        .light {
            position: absolute;
            width: 80px;
            height: 80px;
            border-radius: 50%;
            background-color: var(--light-color);
            transition: all 0.24s;

        }

        .light::before {
            content: '';
            position: absolute;
            width: 35px;
            height: 80px;
            border-radius: 10px;
            background: var(--light-color);
            left: 27.5%;
            top: -50px;
            border-top: 30px solid black;
        }

        .light span:nth-child(1) {
            position: absolute;
            width: 30px;
            height: 30px;
            background: transparent;
            box-shadow: 20px 20px 0 10px var(--light-color);
            border-bottom-right-radius: 40px;
            left: -4px;
            top: -16px;
            transform: rotate(342deg);
        }

        .light span:nth-child(2) {
            position: absolute;
            width: 30px;
            height: 30px;
            background: transparent;
            box-shadow: -20px 20px 0 10px var(--light-color);
            border-bottom-left-radius: 40px;
            right: -3.4px;
            top: -16px;
            transform: rotate(16deg);
        }

        .wire {
            width: 4px;
            height: 400px;
            background-color: #8f8e8e;
            top: -18%;
            position: absolute;
            transition: all 0.24s;
        }

        .light::after {
            position: absolute;
            content: '';
            width: 140px;
            height: 140px;
            background: var(--light-color);
            border-radius: 50%;
            top: 50%;
            left: 0;
            filter: blur(40px);
            transform: translate(-18%, -40px);
            box-shadow: 0 0 10px var(--light-color),
                0 0 30px var(--light-color),
                0 0 60px var(--light-color),
                0 0 120px var(--light-color),
                0 0 200px var(--light-color),
            ;
        }

        button {
            position: absolute;
            bottom: 240px;
            right: 240px;
            width: 120px;
            height: 36px;
        }
    </style>
</head>

<body>
    <div class="container">
        <div class="light-container">
            <div class="wire"></div>
            <div class="light">
                <span></span>
                <span></span>
            </div>
        </div>
    </div>
    <button>开关按钮</button>
    <script>
        let switchOn = true
        let btn = document.querySelector('button')
        let light = document.querySelector('.light')
        let wire = document.querySelector('.wire')
        btn.onclick = () => {
            switchOn = !switchOn
            if (switchOn) {
                document.documentElement.style.setProperty('--light-color', '#fff')
                wire.style.background = '#8f8e8e'
                document.styleSheets[0].addRule('.light::before', 'border-top: 30px solid #000');
            } else {
                document.documentElement.style.setProperty('--light-color', '#333')
                wire.style.background = '#333'
                document.styleSheets[0].addRule('.light::before', 'border-top: 30px solid #333');
            }
        }
        // 使用js动态给伪元素设置样式，参见文章：http://t.zoukankan.com/kunmomo-p-12358005.html
        // 另外样式表也是一个对象，也可以打印 document.querySelector('style') 可访问其上的css属性
    </script>
</body>

</html>
```

## 18.鼠标悬浮手风琴样式展开图标效果图

效果图

![img](https://segmentfault.com/img/bVc4uqk)

代码

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        body {
            padding: 180px;
            background-color: #ddd;
        }

        .item {
            box-sizing: border-box;
            display: inline-flex;
            align-items: center;
            height: 60px;
            /* 手风琴效果就是鼠标悬浮宽度过渡 */
            width: 60px;
            margin: 4px 8px;
            /* 超出隐藏，因为要把伪元素文字遮挡住 */
            overflow: hidden;
            background: #fff;
            border-radius: 30px;
            box-shadow: 0px 10px 10px rgba(0, 0, 0, 0.24);
            transition: all 0.5s;
        }

        .item:hover {
            width: 180px;
            border: none;
        }

        /* 悬浮加背景色 */
        .first:hover .icon {
            background-color: pink;
        }

        .second:hover .icon {
            background-color: #e9e9e9;
        }

        .third:hover .icon {
            background-color: pink;
        }

        .fouth:hover .icon {
            background-color: #e9e9e9;
        }

        .icon {
            width: 60px;
            height: 60px;
            display: flex;
            justify-content: center;
            align-items: center;
            border-radius: 30px;
            font-size: 28px;
            position: relative;
            transition: all 0.5s;
            /* 真实元素阻止鼠标事件，伪元素自动鼠标事件 */
            pointer-events: none;
        }

        /* 通过伪元素添加内容介绍文字 */
        .item:nth-child(1) .icon::after {
            position: absolute;
            content: '我是红桃';
            /* 宽度随着内容自适应 */
            width: fit-content;
            /* 文字不换行 */
            word-break: keep-all;
            /* 设置伪元素文字大小为中等大小 */
            font-size: medium;
            left: 72px;
            /* 真实元素阻止鼠标事件，伪元素自动鼠标事件 */
            pointer-events: auto;
            cursor: pointer;
        }

        .item:nth-child(2) .icon::after {
            position: absolute;
            content: '我是黑桃';
            width: fit-content;
            word-break: keep-all;
            font-size: medium;
            left: 72px;
            pointer-events: auto;
            cursor: pointer;
        }

        .item:nth-child(3) .icon::after {
            position: absolute;
            content: '我是方块';
            width: fit-content;
            word-break: keep-all;
            font-size: medium;
            left: 72px;
            pointer-events: auto;
            cursor: pointer;
        }

        .item:nth-child(4) .icon::after {
            position: absolute;
            content: '我是梅花';
            width: fit-content;
            word-break: keep-all;
            font-size: medium;
            left: 72px;
            pointer-events: auto;
            cursor: pointer;
        }

        /* 鼠标悬浮加文字下划线（给伪元素添加hover样式） */
        .icon:hover::after {
            text-decoration: underline;
        }
    </style>
</head>

<body>
    <div class="item first">
        <div onclick="clickAfter('红桃')" style="color: #DD3B32;" class="icon">♥</div>
    </div>
    <div class="item second">
        <div onclick="clickAfter('黑桃')" style="color: #1A1A1A;" class="icon">♠</div>
    </div>
    <div class="item third">
        <div onclick="clickAfter('方块')" style="color: #FB1C17;" class="icon">♦</div>
    </div>
    <div class="item fouth">
        <div onclick="clickAfter('梅花')" style="color: #090B0A;" class="icon">♣</div>
    </div>
    <script>
        /**
         * 注意伪元素也可以绑定事件
         *      只需：真实元素 pointer-events: none;
         *            伪元素 pointer-events: auto;
         * 参见文章：https://www.cnblogs.com/letgofishing/p/15987190.html
         * */
        function clickAfter(who) {
            console.log(who);
        }
    </script>
</body>

</html>
```



## 19.用一个标签实现酷炫的CSS动画

原文地址：https://juejin.cn/post/7271969141095235603

原文地址：https://juejin.cn/post/7271070291689750582

![img](/images/html/code/animation/10001.gif)



## 20.12个值得一试的CSS动画

原文地址：https://juejin.cn/post/7223136999851196473

**1.Netflix简介动画**

![img](/images/html/code/animation/10002.gif)

预览地址：https://codepen.io/claudio_bonfati/pen/mdryxPv

**2.Bongo 猫**

![img](/images/html/code/animation/10003.gif)

预览地址：https://codepen.io/carolineartz/pen/qBOEzQa

**3.圣诞树**

![img](/images/html/code/animation/10004.gif)

预览地址：https://codepen.io/chrisgannon/pen/dypvKvR

**4.无限道路**

![img](/images/html/code/animation/10005.gif)

预览地址：https://codepen.io/al-ro/pen/xxxxgxK

**5.矩阵数字雨**

![img](/images/html/code/animation/10006.gif)

预览地址：https://codepen.io/yuanchuan/pen/YoqWeR

**6.永恒之心**

![img](/images/html/code/animation/10007.gif)

预览地址：https://codepen.io/yuanchuan/pen/wZJqNK

**7.策马奔腾**

![img](/images/html/code/animation/10008.gif)

预览地址：https://codepen.io/ste-vg/pen/oKYjKV

**8.冰与火之恋**

![img](/images/html/code/animation/10009.gif)

预览地址：https://codepen.io/al-ro/pen/BaaBage

**9.四季变换**

![img](/images/html/code/animation/10010.gif)

预览地址：https://codepen.io/agathaco/pen/rpZoYd

**10.聚能动物**

![img](/images/html/code/animation/10011.gif)

预览地址：https://codepen.io/ainalem/pen/dKLpBE

**11.土星呼啦圈**

![img](/images/html/code/animation/10012.gif)

预览地址：https://codepen.io/jcoulterdesign/pen/BrdPaw

**12.帕拉克斯日落**

![img](/images/html/code/animation/10013.gif)

预览地址：https://codepen.io/quinlo/pen/XPVmVj



## 21.CSS实现10种鼠标移入按钮动效

**html代码**

```html
<!DOCTYPE <!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <title>按钮背景动画</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link rel="stylesheet" type="text/css" media="screen" href="index.css" />
</head>

<body>
    <div class="box">
        <div class="title">鼠标移入按钮多种动效</div>
        <div class="btn-list">
            <ul>
                <li>
                    <a class="btn btn1" href="javascript:;"><span>鼠标移入</span>
                        <div class="btnbg"></div>
                    </a>
                    <a class="btn btn2" href="javascript:;"><span>鼠标移入</span>
                        <div class="btnbg"></div>
                    </a>
                    <a class="btn btn3" href="javascript:;"><span>鼠标移入</span>
                        <div class="btnbg"></div>
                    </a>
                    <a class="btn btn4" href="javascript:;">
                        <span>鼠标移入</span>
                        <div class="btnbg1"></div>
                        <div class="btnbg2"></div>
                        <div class="btnbg3"></div>
                        <div class="btnbg4"></div>
                    </a>
                    <a class="btn btn5" href="javascript:;">
                        <span>鼠标移入</span>
                        <div class="btnbg1"></div>
                        <div class="btnbg2"></div>
                    </a>
                    <a class="btn btn6" href="javascript:;">
                        <span>鼠标移入</span>
                        <div class="btnbg1"></div>
                        <div class="btnbg2"></div>
                        <div class="btnbg3"></div>
                        <div class="btnbg4"></div>
                    </a>
                    <a class="btn btn7" href="javascript:;">
                        <span>鼠标移入</span>
                        <div class="btnbg1"></div>
                        <div class="btnbg2"></div>
                    </a>
                    <a class="btn btn8" href="javascript:;">
                        <span>鼠标移入</span>
                        <div class="btnbg1"></div>
                        <div class="btnbg2"></div>
                    </a>
                    <a class="btn btn9" href="javascript:;">
                        <span>鼠标移入</span>
                        <div class="btnbg1"></div>
                        <div class="btnbg2"></div>
                        <div class="btnbg3"></div>
                        <div class="btnbg4"></div>
                    </a>
                    <a class="btn btn10" href="javascript:;"><span>鼠标移入</span>
                        <div class="btnbg"></div>
                    </a>
                </li>
            </ul>
        </div>
    </div>
</body>

</html>
```

**css代码**

```css
*{
    margin: 0;
    padding: 0;
}
ul, li{
    list-style: none;
}
a{
    color: #ccc;
    text-decoration: none;
}
.box{
    background: #30303c;
    width: 100%;
    height: 100%;
}
.title{
    color: #fff;
    text-align: center;
    font-size: 20px;
    padding: 20px 0;
}
.btn-list{
    margin: 50px auto;
    width: 800px;
}

.btn{
    padding: 10px 40px;
    font-size: 14px;
    overflow: hidden;
    display: inline-block;
    margin: 7px;
}

/* 1 */
.btn1{
    border: 1px solid #ccc;
    position: relative; /* 相对 */
    transition: all 0.5s; /* 过度 */
    -moz-transition: all 0.5s; /* Firefox */
    -webkit-transition: all 0.5s; /* Safari 和 Chrome */
}
.btn1 .btnbg{
    position: absolute; /* 绝对 */
    left: 50%;
    width: 0;
    top: 0;
    bottom: 0;
    transition: all 0.5s; /* 过度 */
    -moz-transition: all 0.5s; /* Firefox */
    -webkit-transition: all 0.5s; /* Safari 和 Chrome */
    background: #f55336;
}
.btn1:hover{
    border-color: #f55336;
    color: #fff;
}
.btn1:hover .btnbg{
    width: 100%;
    left: 0;
}
.btn1 span{
    position: relative;
    z-index: 1;
}

/* 2 */
.btn2{
    /* transform 属性向元素应用 2D 或 3D 转换。该属性允许我们对元素进行旋转、缩放、移动或倾斜 */
    /* translateZ(z) 定义 3D 转换，只是用 Z 轴的值 */
    /* perspective(n) 为 3D 转换元素定义透视视图 */
    transform: perspective(1px) translateZ(0);
    -webkit-transform: perspective(1px) translateZ(0);
    /* transition-property 属性规定应用过渡效果的 CSS 属性的名称 */
    transition-property: color;
    -webkit-transition-property: color;
    transition-duration: 0.5s; /* 过渡效果持续多长时间 */
    -webkit-transition-duration: 0.5s;
    border: 1px solid #ccc;
    position: relative; /* 相对 */
}
.btn2:hover{
    border-color: #ffca28;
    color: #fff;
}
.btn2 .btnbg{
    background: #ffca28;
    position: absolute;
    z-index: -1;
    top: -1px;
    left: -1px;
    right: -1px;
    bottom: -1px;
    /* 通过设置 X 轴的值来定义缩放转换 */
    transform: scaleX(0);
    -webkit-transform: scaleX(0);
    /* 允许改变被转换元素的位置 */
    transform-origin: 0 50%;
    -webkit-transform-origin: 0 50%;
    /* 过渡效果持续 */
    transition-duration: 0.5s;
    -webkit-transition-duration: 0.5s;
    /* 规定过渡效果的速度曲线 */
    /* ease-out 以慢速结束的过渡效果（等于 cubic-bezier(0,0,0.58,1)） */
    transition-timing-function: ease-out;
    -webkit-transition-timing-function: ease-out;
    opacity: 0;
    filter: alpha(opacity=0);
}
.btn2:hover .btnbg{
    /* 规定过渡效果的速度曲线 */
    /* ease-out 以慢速结束的过渡效果（等于 cubic-bezier(0,0,0.58,1)） */
    transition-timing-function: cubic-bezier(0.52,1.64,0.37,0.66);
    -webkit-transition-timing-function: cubic-bezier(0.52,1.64,0.37,0.66);
    /* scaleX 表示水平方向缩放的倍数 */
    transform: scaleX(1);
    -webkit-transform: scaleX(1);
    opacity: 1;
    filter: alpha(opacity=100);
}

/* 3 */
.btn3{
    border: 1px solid #ccc;
    position: relative; /* 相对 */
    transition: border-color .3s, color .3s;
    -webkit-transition: border-color .3s, color .3s;
    /* 规定过渡效果的速度曲线 */
    transition-timing-function: cubic-bezier(.2,1,.3,1);
    -webkit-transition-timing-function: cubic-bezier(.2,1,.3,1);
}
.btn3:hover{
    color: #fff;
    border-color: #d500f9;
}
.btn3 .btnbg{
    background: #d500f9;
    position: absolute;
    top: 0;
    left: 0;
    width: 150%;
    height: 100%;
    z-index: 1;
    opacity: 0;
    filter: alpha(opacity=0);
    /* 旋转 div 元素 */
    transform: rotate3d(0,0,1,-45deg) translate3d(0,-3em,0);
    -webkit-transform: rotate3d(0,0,1,-45deg) translate3d(0,-3em,0);
    /* 设置旋转元素的基点位置 */
    transform-origin: 0% 100%;
    -webkit-transform-origin: 0% 100%;
    transition: transform .3s, opacity .3s;
    -webkit-transform: -webkit-transform .3s, opacity .3s;
}
.btn3:hover .btnbg{
    opacity: 1;
    filter: alpha(opacity=100);
    /* 旋转 div 元素 */
    transform: rotate3d(0,0,1,0deg);
    -webkit-transform: rotate3d(0,0,1,0deg);
    /* 规定过渡效果的速度曲线 */
    transition-timing-function: cubic-bezier(.2,1,.3,1);
    -webkit-transition-timing-function: cubic-bezier(.2,1,.3,1);
}
.btn3 span{
    position: relative;
    z-index: 2;
}

/* 4 */
.btn4{
    border: 1px solid #ccc;
    position: relative; /* 相对 */
    transition: all .4s;
    -webkit-transition: all .4s;
}
.btn4:hover{
    color: #fff;
    border-color: #f06292;
}
.btn4 .btnbg1, .btn4 .btnbg2, .btn4 .btnbg3, .btn4 .btnbg4{
    background: #f06292;
    position: absolute;
    width: 25%;
    height: 0;
    /* 是一个简写属性，用于设置四个过渡属性 */
    transition: height .4s;
    -webkit-transition: height .4s;
}
.btn4 .btnbg1{
    top: 0;
    left: 0;
}
.btn4 .btnbg2{
    bottom: 0;
    left: 25%;
}
.btn4 .btnbg3{
    top: 0;
    left: 50%;
}
.btn4 .btnbg4{
    bottom: 0;
    left: 75%;
}
.btn4:hover .btnbg1, .btn4:hover .btnbg2, .btn4:hover .btnbg3, .btn4:hover .btnbg4{
    height: 100%;
}
.btn4 span{
    position: relative;
    z-index: 1;
}

/* 5 */
.btn5{
    border: 1px solid #ccc;
    position: relative; /* 相对 */
    transition: all .5s;
    -webkit-transition: all .5s;
}
.btn5:hover{
    border-color: #ff5252;
    color: #fff;
}
.btn5 .btnbg1, .btn5 .btnbg2{
    content: '';
    width: 0;
    height: 0;
    /* 属性向元素应用 2D 或 3D 转换。该属性允许我们对元素进行旋转、缩放、移动或倾斜 */
    transform: rotate(360deg);
    -webkit-transform: rotate(360deg);
    border-style: solid;
    border-width: 0;
    /* transparent 用来指定全透明色彩 */
    border-top-color: transparent;
    border-bottom-color: transparent;
    position: absolute;
    /* 过渡 */
    transition: all 0.6s;
    -webkit-transition: all 0.6s;
}
.btn5 .btnbg1{
    border-right-color: transparent;
    border-left-color: #ff5252;
    bottom: 0;
    left: 0;
}
.btn5 .btnbg2{
    /* transparent 用来指定全透明色彩 */
    border-left-color: transparent; 
    border-right-color: #ff5252;
    top: 0;
    right: 0;
}
.btn5:hover .btnbg1{
    border-width: 200px 0 0 200px;
}
.btn5:hover .btnbg2{
    border-width: 0 200px 200px 0;
}
.btn5 span{
    position: relative;
    z-index: 1;
}

/* 6 */
.btn6{
    border: 1px solid #ccc;
    position: relative; /* 相对 */
    /* transition过渡 */
    transition: all .6s;
    -webkit-transition: all .6s;
}
.btn6:hover{
    border-color: #40c4ff;
    color: #fff;
}
.btn6 .btnbg1, .btn6 .btnbg2, .btn6 .btnbg3, .btn6 .btnbg4{
    content: '';
    width: 0;
    height: 0;
    /* 旋转 div 元素 */
    transform: rotate(360deg);
    -webkit-transform: rotate(360deg);
    border-style: solid;
    border-width: 0;
    position: absolute;
    transition: all 0.6s;
    -webkit-transition: all 0.6s;
}
.btn6 .btnbg1{
    border-top-color: transparent;
    border-right-color: transparent;
    border-bottom-color: transparent;
    border-left-color: #40c4ff;
    bottom: 0;
    left: 0;
}
.btn6 .btnbg2{
    border-top-color: #40c4ff;
    border-right-color: transparent;
    border-bottom-color: transparent;
    border-left-color: transparent;
    top: 0;
    left: 0;
}
.btn6 .btnbg3{
    border-top-color: transparent;
    border-right-color: #40c4ff;
    border-bottom-color: transparent;
    border-left-color: transparent;
    top: 0;
    right: 0;
}
.btn6 .btnbg4{
    border-top-color: transparent;
    border-right-color: transparent;
    border-bottom-color: #40c4ff;
    border-left-color: transparent;
    bottom: 0;
    right: 0;
}
.btn6:hover .btnbg1{
    border-width: 200px 0 0 200px;
}
.btn6:hover .btnbg2{
    border-width: 200px 200px 0 0;
}
.btn6:hover .btnbg3{
    border-width: 0 200px 200px 0;
}
.btn6:hover .btnbg4{
    border-width: 0 0 200px 200px;
}
.btn6 span{
    position: relative;
    z-index: 1;
}

/* 7 */
.btn7{
    border: 1px solid #ccc;
    position: relative; /* 相对 */
    transition: all .6s;
    -webkit-transition: all .6s;
}
.btn7:hover{
    border-color: #00e676;
    color: #fff;
}
.btn7 .btnbg1, .btn7 .btnbg2{
    background: #00e676;
    position: absolute;
    top: 50%;
    top:0/9;
    content: '';
    width: 20px;
    height: 20px;
    border-radius: 10px;
    transition: all .6s;
    -webkit-transition: all .6s;
    opacity: 0.5;
}
.btn7 .btnbg1{
    left: -20px;
    /* translate(-50%,-50%) 作用是，往上（x轴）,左（y轴）移动自身长宽的 50%，以使其居于中心位置 */
    transform: translate(-50%,-50%);
    -webkit-transform: translate(-50%,-50%);
}
.btn7 .btnbg2{
    right: -20px;
    transform: translate(50%,-50%);
    -webkit-transform: translate(50%,-50%);
}
.btn7:hover .btnbg1{
    opacity: 1;
    animation: criss-cross-left .9s both;
    -webkit-animation: criss-cross-left .9s both;
    width: 375px/9;
    height: 375px/9;
}
.btn7:hover .btnbg2{
    opacity: 1;
    animation: criss-cross-right .9s both;
    -webkit-animation: criss-cross-right .9s both;
    width: 375px/9;
    height: 375px/9;
}
.btn7 span{
    position: relative;
    z-index: 1;
}
@keyframes criss-cross-left{
    0%{
        left: -20px;
    }
    50%{
        left: 50%;
        width: 20px;
        height: 20px;
    }
    100%{
        left: 50%;
        width: 375px;
        height: 375px;
    }
}
@-webkit-keyframes criss-cross-left{
    0%{
        left: -20px;
    }
    50%{
        left: 50%;
        width: 20px;
        height: 20px;
    }
    100%{
        left: 50%;
        width: 375px;
        height: 375px;
    }
}
@keyframes criss-cross-right{
    0%{
        right: -20px;
    }
    50%{
        right: 50%;
        width: 20px;
        height: 20px;
    }
    100%{
        right: 50%;
        width: 375px;
        height: 375px;
    }
}
@-webkit-keyframes criss-cross-right{
    0%{
        right: -20px;
    }
    50%{
        right: 50%;
        width: 20px;
        height: 20px;
    }
    100%{
        right: 50%;
        width: 375px;
        height: 375px;
    }
}

/* 8 */
.btn8{
    border: 1px solid #ccc;
    position: relative; /* 相对 */
    transition: all .6s;
    -webkit-transition: all .6s;
}
.btn8:hover{
    border-color: #009688;
    color: #fff;
}
.btn8 .btnbg1, .btn8 .btnbg2{
    content: '';
    width: 0;
    height: 0;
    transform: rotate(360deg);
    -webkit-transform: rotate(360deg);
    border-style: solid;
    border-width: 0;
    border-top-color: transparent;
    border-bottom-color: transparent;
    background: #009688;
    position: absolute;
    transition: all .6s;
    -webkit-transition: all .6s;
}
.btn8 .btnbg1{
    border-right-color: transparent;
    border-left-color: #009688;
    bottom: 0;
    left: 0;
}
.btn8 .btnbg2{
    border-right-color:#009688;
    border-left-color: transparent;
    top: 0;
    right: 0;
}
.btn8:hover .btnbg1{
    border-width: 50px 260px;
}
.btn8:hover .btnbg2{
    border-width: 50px 260px;
}
.btn8 span{
    position: relative;
    z-index: 1;
}

/* 9 */
.btn9{
    border: 1px solid #ccc;
    position: relative; /* 相对 */
    transition: all .6s;
    -webkit-transition: all .6s;
}
.btn9:hover{
    border-color: #2979ff;
    color: #fff;
}
.btn9 .btnbg1, .btn9 .btnbg2, .btn9 .btnbg3, .btn9 .btnbg4{
    background: #2979ff;
    position: absolute;
    top: 0;
    width: 0;
    height: 100%;
    transition: all .4s;
    -webkit-transition: all .4s;
    opacity: 0.35;
}
.btn9 .btnbg3, .btn9 .btnbg4{
    opacity: 0.75;
}
.btn9 .btnbg1{
    left: 0;
}
.btn9 .btnbg2{
    right: 0;
}
.btn9 .btnbg3{
    right: 0;
}
.btn9 .btnbg4{
    left: 0;
}
.btn9:hover .btnbg1, .btn9:hover .btnbg2, .btn9:hover .btnbg3, .btn9:hover .btnbg4{
    width: 100%;
}
.btn9:hover .btnbg3, .btn9:hover .btnbg4{
    /* 过渡效果开始前等待 0.4 秒 */
    transition-delay: .4s;
    -webkit-transition-delay: .4s;
}
.btn9 span{
    position: relative;
    z-index: 1;
}
/* 10 */
.btn10{
    border: 1px solid #ccc;
    position: relative; /* 相对 */
    transition: all .6s;
    -webkit-transition: all .6s;
}
.btn10:hover{
    border-color: #00e5ff;
    color: #fff;
}
.btn10 .btnbg{
    background: #00e5ff;
    position: absolute;
    width: 0;
    height: 0;
    border-radius: 50%;
    /* translate(-50%,-50%) 作用是，往上（x轴）,左（y轴）移动自身长宽的 50%，以使其居于中心位置 */
    transform: translate(-50%,-50%);
    -webkit-transform: translate(-50%,-50%);
    transition: width .6s,height .6s;
    -webkit-transition: width .6s,height .6s;
    left: 0;
    top: 0;
}
.btn10:hover .btnbg{
    width: 600px;
    height: 600px;
}
.btn10 span{
    position: relative;
    z-index: 1;
}
```



## 22.HTML5 WebGL 3D樱花飘落动画

- 原文链接：[在线地址](https://www.html5tricks.com/html5-webgl-sakura-animation.html)

- 源码链接：[在线地址](https://www.html5tricks.com/download/pure-css-accordion-menu.rar)

- 在线演示：[在线地址](https://www.html5tricks.com/demo/pure-css-accordion-menu/index.html)

![img](/images/html/code/animation/html5-webgl-sakura-animation.png)



## 23.hover动画效果合集

- 默认语言：English
- 源码地址：https://codepen.io/MoYu1991/pen/avgKxV
- 演示地址：https://codepen.io/MoYu1991/pen/avgKxV

![img](/images/html/code/animation/10014.png)



##  24.聚焦光标文本

- 源码地址：[在线地址](https://codepen.io/carolineartz/pen/rNaGQYo)

- 演示地址：[在线地址](https://codepen.io/carolineartz/pen/rNaGQYo)

![img](/images/html/code/animation/10015.png)



