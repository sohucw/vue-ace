# 背景

前期我是用的 [vue2-ace](https://runkit.com/npm/vue2-ace) 用的过程当中发现了问题:
代码里面的
```
      vm.$parent.$emit('editor-update', editor.getValue());
```

如果你是在组件中引入了 [vue2-ace](https://runkit.com/npm/vue2-ace)   你的组件和他形成父子关系这样是没问题的
如果你的组件的子组件引入了的话 类似形成  爷-子-孙的关系 甚至更深的关系  代码里面的 vm.$parent.$emit() 这种触发方式是用问题的.
所以在原来作者的基础之上做了小的调整 (主要是监听输入的内容的变化)


# vue-ace

A Vue2 component for including the [ace editor](https://ace.c9.io/).

### 安装

```
npm install -save vue-ace
```

### 怎么使用

引入 component,   mode  theme in `<script>`.

mode 语法校验 JavaScript  java sql  ejs ..

theme 主题风格

```
import editor from 'vue-ace'
import 'brace/mode/javascript'
import 'brace/theme/chrome'
```

注册 component 在 Vue 选项.

```
components: {
  editor
}
```

使用组件在你的template中,  确保参数是字符串 加上引号 如

```
<editor :content="需要初始化的内容" :lang="'sql'" :theme="'chrome'" ></editor>
```


下面是参数 默认的是下面的

```
lang: javascript
theme: chrome
height: 300px
width: 100%
```


下面的是使用的几种方式

```
<editor :content="variable" :height="'500px'"></editor>

<editor :content="variable" :width="'50%'"></editor>

<editor :content="variable" :lang="'html'"></editor>

<editor :content="variable" :theme="'github'"></editor>

<editor :content="variable" :sync="true"></editor>
```

你也可以使用其他的模板 类似这样的引入

 ```
   import 'brace/mode/javascript';  //语法校验
   import 'brace/theme/chrome'; // 主题

 ```


下面是是关键的怎么监听用户输入的内容

在父组件中

```
<template >

 <editor v-bind:content-update="XXX"></editor>
</template>

<script>

components: {
  editor
}
methods: {
      XXX: function (v) {
        console.log(v);
      }

    }
</script>
```
### 效果


![demo](https://github.com/sohucw/vue-ace/blob/master/demo.png)





