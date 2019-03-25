# DOM 学习和填的坑
## 1. 操作DOM
- **DOM定位获取方法**
![DOM 思维导图]( DOM思维导图.png )
- **xpath定位的坑**
* [selenium —— 父子、兄弟、相邻节点定位方式详解](https://blog.csdn.net/huilan_same/article/details/52541680)
* [selenium —— 上传文件处理标签被隐藏](https://www.cnblogs.com/hanmk/p/8215809.html)
- **xpath语法总结**
* XPath 轴

| 轴名称                | 结果                           |
|--------------------|------------------------------|
| ancestor           | 选取当前节点的所有先辈（父、祖父等）。          |
| ancestor-or-self   | 选取当前节点的所有先辈（父、祖父等）以及当前节点本身。  |
| attribute          | 选取当前节点的所有属性。                 |
| child              | 选取当前节点的所有子元素。                |
| descendant         | 选取当前节点的所有后代元素（子、孙等）。         |
| descendant-or-self | 选取当前节点的所有后代元素（子、孙等）以及当前节点本身。 |
| following          | 选取文档中当前节点的结束标签之后的所有节点。       |
| namespace          | 选取当前节点的所有命名空间节点。             |
| parent             | 选取当前节点的父节点。                  |
| preceding          | 选取文档中当前节点的开始标签之前的所有节点。       |
| preceding-sibling  | 选取当前节点之前的所有同级节点。             |
| self               | 选取当前节点。                      |

_**实例**_
| 例子                     | 结果                                      |
|------------------------|-----------------------------------------|
| child::book            | 选取所有属于当前节点的子元素的 book 节点。                |
| attribute::lang        | 选取当前节点的 lang 属性。                        |
| child:: *              | 选取当前节点的所有子元素。                           |
| attribute:: *          | 选取当前节点的所有属性。                            |
| child::text()          | 选取当前节点的所有文本子节点。                         |
| child::node()          | 选取当前节点的所有子节点。                           |
| descendant::book       | 选取当前节点的所有 book 后代。                      |
| ancestor::book         | 选择当前节点的所有 book 先辈。                      |
| ancestor-or-self::book | 选取当前节点的所有 book 先辈以及当前节点（如果此节点是 book 节点） |
| child:: */child::price | 选取当前节点的所有 price 孙节点。                    |

* _Xpath 语法_

| Column A | Column B                      |
|----------|-------------------------------|
| nodename | 选取此节点的所有子节点。                  |
| /        | 从根节点选取。                       |
| //       | 从匹配选择的当前节点选择文档中的节点，而不考虑它们的位置。 |
| .        | 选取当前节点。                       |
| ..       | 选取当前节点的父节点。                   |
| @        | 选取属性                          |

* _xpath 一些函数和例子_

**html实例**
```
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>建立测试网址文本</title>
</head>
<body>
<div id="content" version="1.0">
    <ul id="useful">
        <li>数学建模方法</li>
        <li>数学建模数据</li>
        <li>数学建模软件</li>
    </ul>
    <ul id="useless">
        <li>不需要的信息１</li>
        <li>不需要的信息２</li>
        <li>不需要的信息３</li>
    </ul>
     <book>
        <title lang="eng">数学建模书籍1</title>
        <price>29.99</price>
    </book>
    <book>
        <title lang="eng">数学建模书籍2</title>
        <price>39.95</price>
     </book>
    <div id="url">
        <a href="http:nveyun.com">虐云建模网</a>
        <a href="http://nveyun.com/forum.php" title="虐云建模论坛">建模论坛</a>
    </div>
</div>
</body>
</html>
```
_代码片段_：
[last()-1]：表示选择的倒数第二个book子元素
book_last=selector.xpath('//book[last()]/title[@lang="eng"]/text()')
[position()< 3] ：表示选择前两个book子元素
book_p=selector.xpath('//book[position()< 3]/title[@lang="eng"]/text()')
//title[@lang] ：表示选择所有具有lang属性的title节点
lang=selector.xpath('//title[@lang]/text()')
运算符：and 和 or   [@class='a'  or @class='b']
部分匹配可以用contains
