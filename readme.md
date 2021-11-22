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
    new Vue({
        el: '#root',
        data:{
            name:'弗里德里克'
        }
    })
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
