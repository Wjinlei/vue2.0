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
        <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script> <!-- 引入vue.js,开发模式 -->
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
        <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
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
        <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
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
                    // getter
                    get: function() {
                        return this.msg
                    },
                    // setter
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

### 条件渲染
- v-if
```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width" />
        <title>条件渲染</title>
        <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    </head>
    <body>
        <div id="example">
            <div v-if="count == 5"> <!-- 当count == 5 -->
                v-if: {{ count }}<br/>
            </div>
            <div v-else-if="count == 10"> <!-- 当count == 10 -->
                v-else-if: {{ count }}
            </div>
            <div v-else> <!-- 其他情况 -->
                v-else: {{ count }}
            </div>
        </div>
    <script charset="utf-8">
        var vm = new Vue({
            el: '#example',
            data: {
                count: 0,
            }
        })
    </script>
    </body>
</html>
```
- v-show
```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width" />
        <title>条件渲染</title>
        <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    </head>
    <body>
        <div id="example">
            <div v-show="count == 3">
                v-show: {{ count }} <!-- v-show 的元素始终会被渲染并保留在 DOM 中。v-show 只是简单地切换元素的 CSS 属性 display。-->
            </div>
            <!--
v-if vs v-show

v-if 是“真正”的条件渲染，因为它会确保在切换过程中条件块内的事件监听器和子组件适当地被销毁和重建。

v-if 也是惰性的：如果在初始渲染时条件为假，则什么也不做——直到条件第一次变为真时，才会开始渲染条件块。

相比之下，v-show 就简单得多——不管初始条件是什么，元素总是会被渲染，并且只是简单地基于 CSS 进行切换。

一般来说，v-if 有更高的切换开销，而 v-show 有更高的初始渲染开销。因此，如果需要非常频繁地切换，则使用 v-show 较好；如果在运行时条件很少改变，则使用 v-if 较好。
            -->
        </div>
    <script charset="utf-8">
        var vm = new Vue({
            el: '#example',
            data: {
                count: 0,
            }
        })
    </script>
    </body>
</html>
```

### 列表渲染
```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width" />
        <title>列表渲染</title>
        <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    </head>
    <body>
        <div id="example">
            <!-- 对list做遍历,item是每次遍历的元素,这和其他语言的for循环基本一样没什么可说的 -->
            <div v-for="item in list">{{ item.name }}</div>

            <hr/>

            <!-- v-if和v-for一起使用 -->
            <div v-for="item in list">
                <div v-if="item.age > 30"> <!-- age 大于30的显示名字 -->
                    {{ item.age }}
                </div>
                <div v-else> <!-- 否则显示名字 -->
                    {{ item.name }}
                </div>
            </div>
        </div>
    <script charset="utf-8">
        var vm = new Vue({
            el: '#example',
            data: {
                list: [
                    {name: 'zhangSan', age: 20},
                    {name: 'liSi', age: 30},
                    {name: 'wangWu', age: 35}
                ]
            }
        })
    </script>
    </body>
</html>
```

### Class与Style绑定
- `class`绑定
```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width" />
        <title>Class与Style绑定</title>
        <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    </head>
    <body>
        <div id="example">
            <div v-bind:class="{ active: isActive }"></div> <!-- active这个class是否存在,取决于isActive这个属性是否是true -->
            <div class="status" v-bind:class="{ active: isActive }"></div> <!-- v-bind:class 指令也可以与普通的 class 属性共存-->
            <div v-bind:class="classObj"></div> <!-- 绑定的数据对象也可不必内联定义在模板里,这里绑定一个classObj的数据对象 -->
            <div v-bind:class="classObj2"></div> <!-- 你还可以绑定一个计算属性 -->
            <div v-bind:class="[arrActive, arrClass]"></div> <!-- 你还可以传递一个数组来指定class列表 -->
            <div v-bind:class="[isActive ? arrActive : '', arrClass]"></div> <!-- 当isActive为true时,才添加arrActive -->
            <div v-bind:class="[{active : isActive}, arrClass]"></div> <!-- 当isActive为true时,才添加arrActive -->
        </div>
    <script charset="utf-8">
        var vm = new Vue({
            el: '#example',
            data: {
                isActive: true,
                isError: false,
                arrActive: 'active',
                arrClass: 'error',
                classObj: {
                    'active': true,
                    'text-danger': true
                }
            },
            computed: {
                classObj2: function() {
                    return {
                        'active': this.isActive && !this.isError // 当vm.isActive为true和 vm.error为false的时候,才会存在active类名
                    }
                }
            }
        })
    </script>
    </body>
</html>
```
- `style`绑定
```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width" />
        <title>Class与Style绑定</title>
        <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    </head>
    <body>
        <div id="example">
            <!-- 内联写法 -->
            <div v-bind:style="{ color: testColor1, fontSize: testFontSize1 + 'px' }">测试div1</div>
            <!-- 直接绑定到一个样式对象 -->
            <div v-bind:style="styleObj">测试div2</div>
            <!-- 数组写法, 可以将多个样式对象应用到同一个元素上 -->
            <div v-bind:style="[baseStyles, overridingStyles]">测试div3</div> <!-- 如果有多个样式属性相同,则最后一个生效 -->
        </div>
    <script charset="utf-8">
        var vm = new Vue({
            el: '#example',
            data: {
                testColor1: 'red',
                testFontSize1: 30,

                styleObj: {
                    color: 'red',
                    fontSize: '50px'
                },

                baseStyles: {
                    color: 'green',
                    fontSize: '50px'
                },

                overridingStyles: {
                    color: 'yellow',
                    fontSize: '30px'
                }
            }
        })
    </script>
    </body>
</html>
```

### Vue项目的创建
- `vue-cli` 2.x 脚手架
```shell
vue create
```
- `@vue/cli` 3.x 脚手架
```shell
vue ui
```

### 阅读Vue风格指南
- 重点看优先级`A`和优先级`B`的, 地址: `https://cn.vuejs.org/v2/style-guide/`

