# catpl，一个快速可靠的 javascript 模板引擎

## 1.简述

![catpl](https://liyu365.github.io/catpl/catpl.png)

本项目借鉴自artTemplate、juicer、laytpl等诸多项目，在学习这些项目的过程中编写而成。
源码中有大量注释，可以用来学习 javascript 模板引擎的编写。

## 2.使用方式

```
var render = catpl(source);
var html = render(data);
```

`source` 可以是模板字符串或存放有模板字符串的页面元素的id（catpl会根据元素的innerHTML或value属性获取模板字符串）。
生成的 `render` 为一个编译好的函数，可以接收数据对象来生成最终的html。

## 3.配置

该项目目前只有两个配置项：

* `openTag`：逻辑表达式起始标志，默认为{{
* `closeTag`：逻辑表达式关闭标志，默认为}}

可以通过``catpl.set()``方法进行设置，例如：

```
catpl.set('openTag', '{{')
```

或

```
catpl.set({
    openTag : '{{' ,
    closeTag : '}}'
})
```

## 4.赋值语法

对 `< > " ' &` 字符进行转码输出：

```
{{name}}
```

不转码输出：

```
{{#name}}
```

## 5.运算

## 6.条件语法

```
{{if condition}}
    
{{else condition}}
    
{{else}}
    
{{/if}}
```

## 7.遍历语法

```
{{foreach userList as user i}}
    <li>{{i}} : {{user.name}}</li>
{{/foreach}}
```

可以简写为（其中 `$index` 和 `$value` 为固定写法）：

```
{{foreach userList}}
    <li>{{$index}} - {{$value.name}}</li>
{{/foreach}}
```

## 8.包含子模板

嵌入子模板：

```
{{include 'template'}}
```

子模板默认共享当前数据，也可以指定当前数据中的某个键下的数据为子模板的渲染数据：

```
{{include 'template' key}}
```

## 9.注册辅助方法

为 catpl 注册公用的辅助方法：

```
catpl.helper('fun_name', function (date, param) {
    // ..
    return date;
});
```

模板中使用辅助方法的语法：

```
{{data_name | fun_name:'param1','param2'}}
```

可以连续使用多个辅助方法，调用顺序为从左至右：

```
{{data_name | fun_name1:'param1','param2' | fun_name2 | fun_name3}}
```

> 注意 '|' 字符左右的空格不能缺少

## 10.License

**Under MIT license. Copyright by 李昱(liyu365)**