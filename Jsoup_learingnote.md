# Jsoup 入门

标签： 爬虫 java  实习 jsoup

---

> Jsoup是用于解析HTML，就类似XML解析器用于解析XML。 Jsoup它解析HTML成为真实世界的HTML。 它与jquery选择器的语法非常相似，并且非常灵活容易使用以获得所需的结果。
    我们访问某一个网页的时候，在地址栏输入网址，按回车，该网站的服务器就会返回一个HTML文件给我们，浏览器解析返回的数据，展示在UI上。

- 科普：
标签有两种：单标签，双标签

 `<meta ... />`   单标签:设置的数据完全由内部属性给出
`<title> ..  </title>` 双标签:任何一个标签里有属性attr,任何一个属性都有name和value`<metal name=" ..." content=".. " />`

- table布局 
        ```<table>
            <tr> 行
                <td>~</td> 通过表格对齐
            </br>
        </table>```


每一个元素都是一个div，设置class 设置值，在.css 里面设置的具体格式内容


- 定位从谁开始定位： 

    -   根据document 进行定位

    -   element 进行定位


如何定位 

 ``document.getAllElements();`` //所有一级标签

- 根据 DOM 找标签， 多用于element元素找到
- 选择器select() 查找


-------------------------------------------
## select 用法


|描述|测试的HTML代码|写法|
|:-----:|:--------------:|:------------------------|
|通过标签名查找|`<span>33</span> `<br> `<span>25</span>` | Elements elements = doc.select("span");<br><br>注 ：通过标签来查找，直接写 "标签名" 就好， 不需要尖括号|
|通过 id 查找|`<span id="mySpan">36</span>`<br>`<span>20</span>`|Elements elements = doc.select("#mySpan");<br><br> 注 ：通过id来查找，用 `#`|
|通过 class查找|`<span class="myClass">36</span>`<br>`<span>20</span>`|Elements elements = doc.select(".myClass");<br><br>注 ：通过class来查找，用 `.`|
|通过 属性名 查找|`<span class="class1" id="id1">36</span>`<br>`<span class="class2" id="id2">36</span>`|Elements elements = doc<br>.select("span[class=class1]span[id=id1]");<br><br>注 ：查询规则为 标签名[属性名=属性值]，标签名可写可不写，多个属性即多个[]，如上|
|通过 属性名前缀  查找|`<span class="class1">36</span>`<br>`<span class="class2">22</span>`|Elements elements = doc.select("span[^cl]");<br><br>注 ：查询规则为标签名[^属性名前缀] ，<br>标签名可写可不写， 多个属性即多个[]|
|通过 属性名+正则表达式 查找|`<span class="ABC">36</span>`<br>`<span class="ADE">22</span>`|Elements elements = doc.select("span[class~=^AB]");<br><br>注 ：查询规则为 标签名[属性名~=正则表达<br>式]，标签名可写可不写，多个属性即多个[]|
|通过 文本内容 查找|`<span>36</span>`<br>`<span>22</span>`|Elements elements =doc.select("span:contains(3)");<br><br> 注：查询规则为标签名:contains(文本值)|
|通过 文本内容+正则表达式 查找|`<span>36</span>`<br>`<span>22</span>`|Elements elements = doc.select("span:matchesOwn(^3)");<br><br>注 ：查询规则为  标签名:matchesOwn(正则表达式)|




