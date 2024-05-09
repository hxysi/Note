## jQuery

可以直接引用的CDN

[百度CDN](http://libs.baidu.com/jquery/2.1.4/jquery.min.js)

[微软CDN](http://ajax.aspnetcdn.com/ajax/jquery/jquery-2.1.4.min.js)

## jQuery书写位置

 **jQuery 常常位于一个 document ready 函数中：**

```js
$(document).ready(function(){
 
   // 开始写 jQuery 代码...
 
});
```

> [!tip]
>
> ***这是为了防止文档在完全加载（就绪）之前运行 jQuery 代码，即在 DOM 加载完成后才可以对 DOM 进行操作。***
>
> ***如果在文档没有完全加载之前就运行函数，操作可能失败。下面是两个具体的例子：***
>
> - ***试图隐藏一个不存在的元素***
> - ***获得未完全加载的图像的大小***

**简洁写法：**

```js
$(function(){
 
   // 开始写 jQuery 代码...
 
});
```

## 元素选择器

使用美元`$`选择元素：

`$('p')`选择所有的 p 标签
`$('#p')`选择所有id为 p 的标签

`$('.p')`选择所有class为 p 的标签

更多选项：
![image-20240306090152692](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240306090152692.png)

## 效果

### 显示/隐藏





