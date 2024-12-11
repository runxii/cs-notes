当浏览器加载带有 `<script>` 标签的网站时，会发生以下情况：
1. 获取 HTML 页面（例如 _index.html_ ）
2. 开始解析 HTML
3. 解析器遇到引用外部脚本文件的 `<script>` 标记。
4. 浏览器请求脚本文件。同时，解析器会阻止并停止解析页面上的其他 HTML。
5. 一段时间后，脚本被下载并随后执行。
6. 解析器继续解析 HTML 文档的其余部分。

第 4 步会导致糟糕的用户体验。在您下载所有脚本之前，您的网站基本上会停止加载。如果用户讨厌一件事，那就是等待网站加载。

### 为什么会发生这种情况？

任何脚本都可以通过 `document.write()` 或其他 DOM 操作插入自己的 HTML。这意味着解析器必须等到脚本下载并执行后才能安全地解析文档的其余部分。毕竟，脚本 _可以_ 在文档中插入自己的 HTML。

但是，大多数 JavaScript 开发人员不再 _在_ 文档加载时操作 DOM。相反，他们会等到文档加载完毕后再进行修改。例如：

 <!-- index.html -->
 <html>
 <head>
 <title>My Page</title>
 <script src="my-script.js"></script>
 </head>
 <body>
 <div id="user-greeting">Welcome back, user</div>
 </body>
 </html>

JavaScript：
``` js
// my-script.js
document.addEventListener("DOMContentLoaded", function() {
// this function runs when the DOM is ready, ie when the document has been parsed
document.getElementById("user-greeting").textContent = "Welcome back, Bart";
});
```

因为您的浏览器不知道 _my-script.js_ 在下载并执行之前不会修改文档，因此解析器停止解析。

### 过时的推荐

解决这个问题的旧方法是将 `<script>` 标签放在 `<body>` 的底部，因为这样可以确保解析器直到最后都不会被阻塞。

这种方法有其自身的问题：在整个文档被解析之前，浏览器无法开始下载脚本。对于具有大型脚本和样式表的大型网站，能够尽快下载脚本对性能非常重要。如果您的网站在 2 秒内未加载，人们将转到另一个网站。

在最佳解决方案中，浏览器会尽快开始下载您的脚本，同时解析文档的其余部分。

### 现代方法

今天，浏览器支持脚本的 `async` 和 `defer` 属性。这些属性告诉浏览器在下载脚本时继续解析是安全的。

#### 异步
``` js
<script src="path/to/script1.js" async></script>
<script src="path/to/script2.js" async></script>
```

具有 async 属性的脚本是异步执行的。这意味着脚本在下载后立即执行，同时不会阻塞浏览器。
这意味着脚本 2 可能在脚本 1 之前下载并执行。

根据 [http://caniuse.com/#feat=script-async](https://link.segmentfault.com/?enc=CNeNiMIPe4Qz%2FoBTsC%2Fu3w%3D%3D.FdtCLTlFiZxLZlm%2FBGF9FSv%2B3YMOltfvvqnWIyP3s%2B3RggJE8qgl6Ic0DO85J1mH) ，97.78% 的浏览器都支持这一点。

#### 推迟

``` js
<script src="path/to/script1.js" defer></script>
<script src="path/to/script2.js" defer></script>
```

具有 defer 属性的脚本按顺序执行（即首先执行脚本 1，然后执行脚本 2）。这也不会阻止浏览器。

与异步脚本不同，延迟脚本仅在加载整个文档后执行。

根据 [http://caniuse.com/#feat=script-defer](https://link.segmentfault.com/?enc=PrCbksv3rd9XS5Mw0t5f3A%3D%3D.Rfr%2Bfh8a1lpCom7gn0N4vBNmVVrAP%2FuATmlGgaKIISe6%2Bak2Pw3X6MF7GrbDNeLM) ，97.79% 的浏览器都支持这一点。 98.06% 至少部分支持它。

关于浏览器兼容性的重要说明：在某些情况下，Internet Explorer 9 和更早版本可能会乱序执行延迟脚本。如果您需要支持这些浏览器，请先阅读 [此](https://link.segmentfault.com/?enc=MHU%2BW490y7xW2qLcCb%2BB%2BA%3D%3D.TJI1ujZWKNscV4FVxcxSJOXaAAS6xJoN2Anu%2BkVRhNyXnTOQxxceCg%2FPcdO%2F1ViuFRLQAL9tOS55Eid56fPrBQ%3D%3D) 内容！

_（要了解更多信息并查看异步、延迟和普通脚本之间差异的一些非常有用的视觉表示，请查看此答案的参考部分的前两个链接）_

## 结论

当前的最新技术是将脚本放在 `<head>` 标记中并使用 `async` 或 `defer` 属性。这允许您的脚本尽快下载，而不会阻止您的浏览器。

好消息是您的网站仍应在 2% 的不支持这些属性的浏览器上正确加载，同时加快其他 98% 的速度。