### MVC结合了koa处理不同的URL和nunjucks渲染模版

#### mvvm前端技术：model-view-viewmodel
其核心是对view和viewmodel的双向数据绑定

- mvc：
```
Model 其实就是数据。
View 用来把数据以某种方式呈现给用户。
Controller 接收并处理来自用户的请求，并将 Model 返回给用户。
```
- mvvm：
```
Model 层代表数据模型，也可以在Model中定义数据修改和操作的业务逻辑；
View 代表UI 组件，它负责将数据模型转化成UI 展现出来
ViewModel 是一个同步View 和 Model的对象。
```
#### mvvm模型：
```
  1. Model用纯JavaScript对象表示
  2. View负责显示
  3. ViewModel负责把Model的数据同步到View显示出来，还负责把View的修改同步回Model
```
关注点从如何操作DOM变成了如何更新JavaScript对象的状态，
关注Model的变化，让MVVM框架去自动更新DOM的状态，从而把开发者从操作DOM的繁琐步骤中解脱出来！

- 单向绑定：
Vue作为MVVM框架会自动监听Model的任何变化，在Model数据变化时，更新View的显示。
这种Model到View的绑定我们称为单向绑定。
```
另一种单向绑定的方法是使用Vue的指令v-text，写法如下：
<p>Hello, <span v-text="name"></span>!</p>
```
- 双向绑定：
数据双向绑定，当view发生变化时，model作出相应改变，填写表单就是一个最直接的例子
用v-model指令把某个```<input>```和Model的某个属性作双向绑定：
```
<form id="vm" action="#">
    <p><input v-model="email"></p>
    <p><input v-model="name"></p>
</form>
```
表单的v-model的值始终和表单的value属性的值对应
```
//一般的prevent发生在提交表单中
<!-- 提交事件不再重载页面 -->
<form v-on:submit.prevent="onSubmit"></form>
//表示浏览器不再处理submit事件，而是监听submit动作，指定onSubmit方法

把model同步更新到服务器用vue-resource
```