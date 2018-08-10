### 在html中导入一段html代码的功能
需求：不通过后端的include语法，在html中导入一段html代码的功能 
比如项目里有许多通用的html结构，侧边栏导航或者顶部，底部等html结构   

想法：1. 没用过的iframe标签，经实验，很难用，无法实现（弃）  
想法：2. link标签的import这个功能
通过声明 `<link rel="import">` 来在页面中导入html结构，在js里插入到相关节点里。
具体可以看教程 https://www.html5rocks.com/zh/tutorials/webcomponents/imports/   
```
import.html
<div id="top">top</div>
<div id="bottom">bottom</div>
```
```
index.html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <link id="aa" rel="import" href="import.html">
</head>
<body>
<div>index</div>
<script>
    var link = document.querySelector("#aa");
    var content = link.import;
    console.log(link,link.import)

    // 从 warning.html 的文档中获取 DOM。
    var el = content.querySelector('#top');
//这里只会插入#top到内容，#bottom的内容不会插入
    document.body.appendChild(el.cloneNode(true));
</script>
</body>
</html>
```
缺点：兼容性差，目前只有新版chrome支持  
想法3：webpack等工具实现