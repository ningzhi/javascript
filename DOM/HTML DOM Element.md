Title: HTML DOM Element

[TOC]

#DOM中的主要方法

##属性方法


###getAttribute(AttributeName)
获取指定节点的属性值
index.html:
```html
<input type="text" value="姓名" name="name">请输入姓名：
```
script.js
```javascript
var inp=document.getElementsByTagName('input')[0];
    var attr=inp.getAttribute('name');
    alert(attr);
```
效果图：
![t1](img/dom1.jpg)


###removeAttribute(AttributeName)
删除指定节点的属性
```javascript
 var inp=document.getElementsByTagName('input')[0];
    inp.removeAttribute('name');
    var attr=inp.getAttribute('name');
    alert(attr);
```
效果图：
![t2](img/dom2.jpg)


###setAttribute(AttributeName)
设置指定节点的属性值
```javascript
 var inp=document.getElementsByTagName('input')[0];
    inp.setAttribute('name','hello');
    var attr=inp.getAttribute('name');
    alert(attr);
```
效果图：
![t3](img/dom3.jpg)


##节点关系

###childNodes
访问子节点
**该属性返回的是指定节点的全部属性，返回值是一个数组，我们可以通过数组方式访问**
```html
<div id="div1">
        <p>
            我是第一个div的第一个子元素
        </p>
        <p>
            我是第一个div的第二个子元素
        </p>
        <input type="text" value="姓名" name="name">请输入姓名：
    </div>
```
```javascript
  var div1=document.getElementById('div1');
    var child=div1.childNodes;
        alert(child.lenght);
```
效果图：
![t4](img/dom4.jpg)

对于这个结果一开始我也是迷茫的，后来上网查询发现是**在浏览器中节点与节点之间的空格也算一个文本类型的节点**，在一个视频讲解网站上看到只有chrome和firefox中才会将空格算作文本节点，但是经测验，当前使用的主流浏览器都将节点与节点之间的空格算一个文本类型的节点。**如果想要去除这的节点可以将下一个节点的开始标签紧挨着上一个的结尾标签即可。**

```遍历结果：[object text]  [object HTMLParagraphElenent]  [object text]  [object HTMLParagraphElenent]  [object text]  [object HTMLInputElenent]  [object text]```


###firstChild和lastChild
分别表示第一个子节点和最后一个子节点
```html
<table id="tab1">
       <tr>
           <td>1</td>
           <td>1</td>
       </tr>
       <tr>
           <td>2</td>
           <td>2</td>
       </tr>
   </table>
```
```javascript
 var ta=document.getElementById('tab1');
    alert(ta.lastChild.nodeName);
```
效果图：
![t5.1](img/dom5.1.jpg)
![t5.2](img/dom5.2.jpg)
可能结果有点出乎人意料，第一个子节点刚刚已经说过了，而\<table>的最后一个子节点竟然是\<tbody>,所以在这里有一点需要特别注意：**在\<table>元素中有一个默认的\<tbody>元素**，曾经我也是在这里踩过地雷的。


###parentNode
父节点：element.parentNode
祖节点：element.parentNode.parentNode
依次类推
```html
<body>
    <div id="div1">
        <p>
            我是第一个div的第一个子元素
        </p><p>
            我是第一个div的第二个子元素
        </p>
        <input type="text" value="姓名" name="name">请输入姓名：
    </div>
</body>
```
```javascript
  var inp=document.getElementsByTagName('input')[0];
    var p1=inp.parentNode.nodeName;
    var p2=inp.parentNode.parentNode.nodeName;
    alert(p1);
    alert(p2);
```
效果图：
![t6.1](img/dom6.1.jpg)
![t6.2](img/dom6.2.jpg)


###previousSibling
指定节点**之前**紧挨着的兄弟节点

###nextSibling
指定节点**之后**紧跟的兄弟节点

为了让演示效果更加明显我将\<div>中的子节点之间的空格去除
```html
<div id="div1">
        <p>
            我是第一个div的第一个子元素
        </p><p>
            我是第一个div的第二个子元素
        </p><input type="text" value="姓名" name="name">请输入姓名：
    </div>
```
```javascript
var div=document.getElementById('div1');
    var p=div.getElementsByTagName('p')[1];
    alert(p.previousSibling);
    alert(p.nextSibling);
```
效果图：
![t7.1](img/dom7.1.jpg)
![t7.2](img/dom7.2.jpg)


##节点方法
操作的原HTML文档：
```html
<div id="div2">
        <p>
            我是第二个div的第一个子元素
        </p>
        <p>
            我是第二个div的第二个子元素
        </p>
    </div>
```

###createElement(TagName)
创建节点，通常和appendChild()以及inserBefore()一起使用。


###createTextNode(Text)
创建文本节点，返回text字节
```javascript
 var div2=document.getElementById('div2');
    var t=document.createTextNode('我是文本节点');
    div2.appendChild(t);
    alert(t.nodeType);
```
效果图;
![t](img/dom.t.jpg)
![t](img/dom.t.1.jpg)


###appendChild(newNode)
插入新节点**总是在最后加入新节点**
```javascript
   var div2=document.getElementById('div2');
    var newOne=document.createElement('p');
    newOne.innerHTML="我是被新建出来的~~~";
    div2.appendChild(newOne);
```
效果图;
![t8](img/dom8.jpg)


###inserBefore(newNode,oldNode)
在已存在指定**节点前**插入节点

```javascript
var div2=document.getElementById('div2');
    var oldOne=document.getElementsByTagName('p')[1];
    var newOne=document.createElement('p');
     newOne.innerHTML="我是被新建出来的~~~";
    div2.insertBefore(newOne,oldOne);
```
效果图;
![t9](img/dom9.jpg)

**注意：**在调用此方法时，调用的元素应该是newNode和oldNode的**父节点**。


###removeChild(Node)
删除指定节点

```javascript
var div2=document.getElementById('div2');
    var oldOne=document.getElementsByTagName('p')[1];
    var remove=div2.removeChild(oldOne);
    alert(remove.innerHTML);
```
效果图;
![t10](img/dom10.jpg)

**若删除成功返回已删除的节点，失败返回Null,此时的节点虽然能被访问，但是它已经不存在DOM树中，而是在内存里。如果想完全删除可以在代码后面添加`remove=Null;`**


###replaceChild(newNode,oldNode)
替换指定节点

```javascript
 var div2=document.getElementById('div2');
    var oldOne=document.getElementsByTagName('p')[1];
    var newOne=document.createElement('input');
    newOne.style='text';
    newOne.value='请输入';
    div2.replaceChild(newOne,oldOne);
```
效果图;
![t11](img/dom11.jpg)

**注意：**在调用此方法时，调用的元素应该是newNode和oldNode的**父节点**。


#个人总结
* 在通过DOM树结构操作文档节点时，要清楚的知道每一个节点的位置，按层次进行访问。
* 在浏览器中节点与节点之间的空格也算一个文本类型的节点。
* 在\<table>元素中有一个默认的\<tbody>元素。
* getElementsByTagName()和getElementsByName()获取节点的返回值是数组，要按照访问数组的方式进行访问，**下标从0开始**。