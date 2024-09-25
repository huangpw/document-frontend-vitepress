# 滚动加载

## JS实现一款鼠标滚动加载内容的动画效果

![img](/images/javascript/code/roll/10001.gif)

- 原文地址：https://mp.weixin.qq.com/s/KL3_Dp8bDvdjzUx7fxCi1g

HTML代码：

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <link rel="stylesheet" href="style.css" />
        <title>【每日一练】111—JS实现一款鼠标滚动加载内容的动画效果</title>
    </head>
    <body>
        <h1>【每日一练】111—鼠标滚动加载内容的动画</h1>
        <div class="box"><h2>你若想得到这世界最好的东西，</h2></div>
        <div class="box"><h2>先得让世界看到最好的你。</h2></div>
        <div class="box"><h2>努力很难，但要永远记住，</h2></div>
        <div class="box"><h2>如果不努力，就会一直难。</h2></div>
        <div class="box"><h2>你不一定要逆风翻盘，</h2></div>
        <div class="box"><h2>但请一定要向阳而生。</h2></div>
        <div class="box"><h2>有些路，只能一个人走</h2></div>
        <div class="box"><h2>难过的时候记得晒晒太阳</h2></div>
        <div class="box"><h2>生活坏到一定程度就会好起来，</h2></div>
        <div class="box"><h2>因为它无法更坏了！</h2></div>
        <div class="box"><h2>生的再平凡，也是限量版</h2></div>
        <div class="box"><h2>别瞧不起自己！</h2></div>
        <div class="box"><h2>多看书，多走路，</h2></div>
        <div class="box"><h2>心情好了，上班路上都是旅行</h2></div>
        <div class="box"><h2>生活，有太多无能为力和万般无奈</h2></div>
        <div class="box"><h2>可终究还是要努力一点</h2></div>
        <div class="box"><h2>开心一点，想得开一点，</h2></div>
        <div class="box"><h2>毕竟这短短的一生，</h2></div>
        <div class="box"><h2>我们最终都会失去</h2></div>
        <div class="box"><h2>你不妨大胆一些</h2></div>
        <div class="box"><h2>勇敢去爱一个人，</h2></div>
        <div class="box"><h2>去攀一座山，去追一个梦。</h2></div>
        <div class="box"><h2>愿你看透一切，</h2></div>
        <div class="box"><h2>依然心存感激和热爱</h2></div>
        <script src="script.js"></script>
    </body>
</html>
```

CSS代码：

```css
* {
    box-sizing: border-box;
}

body {
    background-color: #fafafa;
    font-family: 'Roboto', sans-serif;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    margin: 0;
    overflow-x: hidden;
}

h1 {
    margin: 10px;
}

.box {
    background-color: #00a6bc;
    color: #fff;
    display: flex;
    align-items: center;
    justify-content: center;
    width: 400px;
    height: 200px;
    margin: 10px;
    border-radius: 10px;
    box-shadow: 2px 4px 5px rgba(0, 0, 0, 0.3);
    transform: translateX(400%);
    transition: transform 0.4s ease;
}

.box:nth-of-type(even) {
    transform: translateX(-400%);
}

.box.show {
    transform: translateX(0);
}

.box h2 {
    font-size: 18px;
    letter-spacing: 5px;
}
```

JS代码：

```js
const boxes = document.querySelectorAll('.box')

window.addEventListener('scroll', checkBoxes)

checkBoxes()

function checkBoxes() {
    const triggerBottom = window.innerHeight / 5 * 4

    boxes.forEach(box => {
        const boxTop = box.getBoundingClientRect().top

        if(boxTop < triggerBottom) {
            box.classList.add('show')
        } else {
            box.classList.remove('show')
        }
    })
}
```

