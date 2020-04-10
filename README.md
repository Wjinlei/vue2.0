### Vue学习前置环境

- `node.js`多版本管理工具`nvm`
```shell
https://github.com/nvm-sh/nvm
```

- 淘宝`npm`镜像`cnpm`
```shell
npm install -g cnpm --registry=https://registry.npm.taobao.org
```

- `vue.js`脚手架`vue-cli`
```shell
sudo npm install -g vue-cli
```

- `vue.js`Chrome插件`Vue.js devtools`

### Hello Vue
```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width" />
        <title>Hello Vue</title>
        <style type="text/css" media="screen">
.bg {
    color: red;
}
        </style>
        <script src="https://cdn.bootcss.com/vue/2.6.11/vue.min.js"></script> <!-- 引入vue.js -->
    </head>
    <body>
        <div id="hello" class="bg">
            {{ msg }} <!-- 输出标签的内容 -->
        </div>
        <script charset="utf-8">
            new Vue({
                el: '#hello', // #hello表示绑定id为hello的元素,还可以用.bg绑定类名
                data: {
                    msg: 'Hello Vue' // 模板标签是msg
                }
            })
        </script>
    </body>
</html>
```
