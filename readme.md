#VUE教程

##初步

###第一课
1.创建一个html容器元素
```html
<div id="root">
    <h1>你好 {{name}}</h1>
</div>
```
2.创建一个vue实例
```javascript
new Vue()
```
3.绑定Vue实例与容器
```javascript
new Vue({
    el: '#root'
})
```
4.设置需要显示的数据
```javascript
绑定方法1: 前期固定绑定
new Vue({
    el: '#root',
    data:{
        name:'弗里德里克'
    }
})

绑定方法2: 后期动态绑定
const app = new Vue({
    data:{
        name:'弗里德里克'
    }
})
app.$mount('#root')
```
>重点
>>1.容器与Vue对象的关系是一一对应

###第二课 模板语法
1. 插值语法,用于解析标签体内容
```javascript
{{变量}}
```
2.指令语法,用于解析标签(包括：标签属性 标签体内容 绑定事件)
```javascript
完整形式
<a v-bind:标签名="值"></a>
简写形式
<a :标签名="值"></a>
```

###第三课 数据绑定
1.单向数据绑定,数据只可以由data流向页面,使用指令语法V-Bind
```javascript
<a v-bind:标签名="值"></a>
```
2.双向数据绑定,数据不仅可以由data流向页面，还可以由页面流向data,使用指令语法V-Model
```javascript
<input type="text" v-model:value="值"></input>
```
>重点
>>双向数据绑定,只可以作用与表单类元素(输入类元素),只对应value属性

###第四课 EL和Data的两种绑定方法
```javascript
绑定方法1: 前期固定绑定
new Vue({
    el: '#root',                            
    data:{                                     
        name:'弗里德里克'                     
    }                                       
})                                          
                                            
绑定方法2: 后期动态绑定
const app = new Vue({
    data: function(){
        return {
                    name: '张三'
                }
    }
})
app.$mount('#root')
```

###第五课 MVVM
####MVVM模型
#####1. M: Model (模型): data中的数据
#####2. V: View (视图): 模板代码
#####3. VM: View-Model (视图模型): vue实例

###第六课 数据代理
####第一节 Object.defineProperty
```javascript
//数据属性描述符(DataDescriptor)和访问器属性描述(AccessorDescriptor)不可以同时出现
Object.defineProperty(person, 'age', {
    //value: 18,                    //数据属性描述符

    //writable: true,               //数据属性描述符
                                    //控制属性是否可以被修改，如果为true则可以被修改，否则不可以，默认值为false

    //enumerable: true,             //控制属性是否可以被枚举，如果为True则可以被遍历,否则不可以被枚举，默认值为false

    //configurable: true,           //控制属性是否可以被删除，如果为true则可以被删除，否则不可以，默认值为false

    get:function (){                //访问器属性描述
                                    //当有人读取age属性时，getter函数被触发，返回值为age的值
        console.log('age的get方法被调用')
        return number;
    },

    set:function (value){           //访问器属性描述
                                    // 当有人设置age属性时，setter函数被触发，且会收到修改的具体值
        console.log('age的set方法被调用, 新值为' + value)
        number = value;
    }
})
```

###第七课 事件绑定   
####第一节 基本使用
1. v-on:事件名 或者 @事件名 绑定事件
2. 事件的回调函数需要配置在methods中
3. methods中使用普通函数(this为vm)，使用箭头函数(this为window)
4. `@click="demo"`与`@click="demo($event,参数1，参数2，参数n)"`等价，如果不写括号，则vue配置一个event参数，如果写了括号，如果想获得event，必须使用$event进行占位传递
####第二节 事件修饰符
1. prevent: 阻止默认事件(常用), 等同于使用 `event.preventDefault()`
2. stop: 阻止事件冒泡
3. once: 事件只触发一次（例如点击以后，再点击不触发事件）
4. capture: 使用事件的捕获模式 默认都是再冒泡阶段触发事件，如果使用捕获模式，则是在捕获阶段触发事件
>    触发过程  
     外层　　　　　　　　　　　　　　　　　　　　　外层      
捕获　1 |                                        |　冒泡触发 6  
　　　中层                                          中层  
捕获 2 |                                         | 冒泡触发 5   
     内层                                           内层  
捕获 3 |---------------------------------------| 冒泡触发 4   
如果是冒泡事件的触发，只会在步骤4/5/6处依次触发
如果是捕获模式触发，则在1/2/3/4/5/6处一次触发
5. self: 只有event.target是当前操作的元素时才触发事件
6. passive: 事件的默认行为立即执行，无需等待事件回调执行完毕，就是一个异步操作的修饰
>修饰符可以连续书写 `@click=prevent.stop`表示不仅阻止默认事件，还阻止事件冒泡
####第三节 键盘事件
1. vue中常用的按键别名
> enter  
> delete(delete和backspace)   
> esc   
> space   
> tab 必须在keydown事件中使用, tab键由于切换焦点的属性，所以如果使用tab键，必须在keydown事件中绑定使用, 否则由于tab键由于焦点切换，导致keyup事件无法触发
> up
> down
> left
> right
2. vue未提供别名的按键，可以使用按键的原始key值去绑定，但是要注意，必须全部转化为小写，如果其中存在大写，使用“-”替换 例如`CapLock->cap-lock`  
3. 系统修饰键: ctrl alt shift meta(window键)  
   a. 配合keydown使用时，只有系统修饰键按下并且再按下其他键时，事件才被触发，单独按下系统修饰键，是不触发keydown事件的，可能是为了兼容快捷键,譬如CTRL+S,保存当前页面
   b. 配合keyup使用时，全部可以正常触发
4. 可以使用keyCode去指定具体的按键，但是再MDN的文档描述中（https://developer.mozilla.org/zh-CN/docs/Web/API/KeyboardEvent/keyCode），keyCode已经被废弃，不建议使用
```javascript
<!-- 使用keyCode去指定具体的按键 -->
<input type="text" placeholder="使用keyCode去指定具体的按键,提示输入" @keyup.32="showInfoKeyUp">
```
6. `Vue.config.keyCodes.自定义键名 = 键码`可以去定制按键别名
```javascript
Vue.config.keyCodes.kongge = 32

<!-- Vue.config.keyCodes.自定义键名 = 键码 定制按键别名 -->
<input type="text" placeholder="使用keyCode去指定具体的按键,提示输入" @keyup.kongge="showInfoKeyUp">
```
>修饰符可以连续书写`<input type="text" placeholder="使用Ctrl+S,提示输入值" @keyup.ctrl.y="showInfoKeyUp">`,这个就是使用ctrl+s作为键值处理
###第八课 计算属性
####第一节 使用插值方法实现
####第二节 使用Methods方法实现
####第三节 使用计算属性实现
1. 定义 
    >需要使用的属性需要依赖已有属性计算得来
2. 原理
    >底层使用了Object.defineproperty方法的setter/getter    
3. get什么时候执行
   >1. 第一次读取时
   >2. 计算时依赖的属性数据发生变化时
4. 优势    
   >内部由缓存机制，效率更高
5. 基本语法
```javascript
computed:{
    待计算的属性,封装成一个对象: {
        get(){
            获得带计算的属性值
        },
        set(value){
            设置计算属性的值
        }
    }
}
```
###第九课 计算属性
###第一节 监视属性基本
1. 什么时候执行
    >当被监视的属性发生变化时，回调函数自动调用
2. 要点
   >被监视的属性必须存在
3. 基本语法
```javascript
    1.静态写法
        watch:{
            // 'weather':{             //标准写法
            //     immediate: true,    //初始化时，是否需要调用
            //     handler(newValue, oldValue){
            //         console.log(oldValue, newValue)
            //     }
            // }
            weather:{
                deep: false;        //是否开启深度监视,可以监测多级变量的变化
                immediate: true,    //初始化时，是否需要调用
                handler(newValue, oldValue){
                    console.log(oldValue, newValue)
                }
            }
        }
    2.动态写法
    vm.$watch('isHot', {
                deep: false;        //是否开启深度监视,可以监测多级变量的变化
                immediate: true,    //初始化时，是否需要调用
                handler(newValue, oldValue){
                    console.log(oldValue, newValue)
                }
            })
```
###第十课 绑定属性
1. 绑定class样式  
```javascript
    class="字符串/对象/数组"

    <!-- 绑定class样式,字符串写法, 适用于样式的类名不确定，需要动态指定 -->
    <div class='basic' :class='样式名字符串' @click="changeMood">绑定class样式-字符串写法</div>
    样式名字符串 = normal

    <!-- 绑定class样式,数组写法, 适用于样式的类名不确定，需要动态指定 -->
    <div class='basic' :class='样式名数组'>绑定class样式-数组写法</div>
    样式名数组 = [italicstyle, fontsizestyle]

    <!-- 绑定class样式,对象写法, 适用于样式个数确定，名字确定，只是动态决定需不需要应用样式 -->
    <div class="basic" :class="样式名对象">绑定class样式-对象写法</div>
    样式名对象 = {
        fontfamilystyle: true,
        fontweightstyle: true,
    }
```
2. 绑定style样式  
```javascript
    <!-- 绑定style样式,对象写法 -->
    <div class="basic" :style="样式对象">绑定style样式-对象写法</div>
    样式对象 = {
        fontSize: '20px',
        color: 'red',
    }

    <!-- 绑定style样式,数组写法 -->
    <div class="basic" :style="数组样式对象">绑定style样式-数组写法</div>
    数组样式对象 = [
        {
            fontSize: '40px',
        },
        {
            color: 'green',
        }
    ]
```
###第十一课 条件渲染
1. v-if/v-else 标签不渲染出来  
2. v-show 标签存在，使用display：none  
3. v-if可以与`<template>`标签配合使用，不会破坏页面结构  
```javascript
<template v-if='n = 1'>
<h2>你好1</h2>
<h2>你好2</h2>
<h2>你好3</h2>
</template>
```
###第十二课 遍历
1. 基本语法
   ```javascript
    v-for="(value, index) in xxx" :key="key">
    value为xxx中的一个基本单元，index为索引号，key为一个基本单元中的一项，且这项必须在列表中处于唯一值
   ```
2. 样例  
   参考part1.html   

##个人心得  
###vue
####函数是否被触发,取决于函数中的变量是否被修改  
####页面是否刷新，取决于虚拟DOM树是否被修改
##javacript
###数组
####基本操作
1. 尾部添加 push
2. 尾部删除 pop
####循环
1. `arr.foreach(item=>{遍历时需要执行的语句})`
####排序
1. `array.sort((value1, value2)=>{  
      if (value1 > value2){
         return 1
      } else {
         if (value1 < value2){
            return -1
         } else {
            return 0 
         }
      } 
   })`
 2.数组反转`arr.reverse()`