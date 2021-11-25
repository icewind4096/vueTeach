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
