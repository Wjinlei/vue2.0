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

### 计算属性computed和侦听器watch
- 通常来说`watch`用来监听一个变量的变化
- `computed`用来可以用来监听多个变量,但这个变量必须在`vue`实例里面
```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width" />
        <title>computed与watch</title>
        <script src="https://cdn.bootcss.com/vue/2.6.11/vue.min.js"></script>
    </head>
    <body>
    <div id="example">
        {{ msg }}
        {{ msg.split('').reverse().join('') }} <!-- 模板内的表达式非常便利，但是设计它们的初衷是用于简单运算的。在模板中放入太多的逻辑会让模板过重且难以维护 -->
        {{ reversedMsg }} <!-- 调用计算属性 -->
    </div>
    <script charset="utf-8">
        var vm = new Vue({
            el: '#example',
            data: {
                msg: 'Hello'
            },
            // watch 表示侦听器
            watch: {
                // 这里声明了一个侦听器侦听msg的变化, 侦听器接收2个值,一个新值,一个旧值,当msg发生变换时将,触发侦听器
                msg: function(newval, oldval){
                    console.log('newval is' + newval)
                    console.log('oldval is' + oldval)
                }
            },
            // computed 计算属性
            computed: {
                // 这里声明了一个reversedMsg计算属性的 getter
                reversedMsg: function() {
                    // `this` 指向 vm 实例,reversedMsg的值会随着msg的更新而变化
                    return this.msg.split('').reverse().join('')
                },
                // 这里声明了一个msg1计算属性的 setter
                msg1: {
                    set: function(value) {
                        // 当msg1这个计算属性发生改变时将修改msg
                        this.msg = value
                    }
                }
            }
        })
    </script>
    </body>
</html>
```
