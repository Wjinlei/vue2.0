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
### 模板
```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width" />
        <title>template</title>
        <style type="text/css" media="screen">
.bg {
    color: red;
}
        </style>
        <script src="https://cdn.bootcss.com/vue/2.6.11/vue.min.js"></script>
    </head>
    <body>
        <div id="hello" class="bg">
            {{ msg }}
            {{ (count +1) * 10 }} <!-- 模板可以计算 -->
            <div v-html="rawhtml"></div> <!-- 通过v-html可以输出html原始代码 -->
            <a v-bind:href="url">跳转到百度</a> <!-- 通过v-bind可以给元素绑定一个属性 v-bind可以缩写为: -->
            <a :href="url1">跳转到Google</a> <!-- v-bind可以缩写为: -->
            <button type="button" v-on:click="submit()">加数字</button> <!-- 通过v-on可以给元素绑定事件 v-on可以缩写为@ -->
            <button type="button" @click="submit2()">加数字2</button> <!-- v-on可以缩写为@ -->
        </div>
        <script charset="utf-8">
            new Vue({
                el: '#hello',
                data: {
                    msg: 'Hello Vue',
                    count: 1,
                    rawhtml: '<div>hello templte</div>',
                    url: 'https://www.baidu.com',
                    url1: 'https://www.google.com',
                },
                methods: {
                    submit: function() {
                        this.count++ // this代表vue对象
                    },
                    submit2: function() {
                        this.count++ // this代表vue对象
                    }
                }
            })
        </script>
    </body>
</html>
```
