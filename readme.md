# html转成pdf，下载(html2canvas)

## html2canvas
## 简介
#### 我们可以直接在浏览器端使用html2canvas,对整个或局部页面进行‘截图’。但这并不是真的截图，而是通过遍历页面DOM结构，收集所有元素信息及相应样式，渲染出canvas image。

#### 由于html2canvas只能将它能处理的生成canvas image，因此渲染出来的结果并不是100%与原来一致。但它不需要服务器参与，整个图片都由客户端浏览器生成，使用很方便。

### 使用

#### 使用的API也很简洁，下面代码可以将某个元素渲染成canvas：

html2canvas(element, {
    onrendered: function(canvas) {
        // canvas is the final rendered <canvas> element
    }
});

#### 通过onrendered方法，可以将生成的canvas进行回调，比如插入到页面中：

html2canvas(element, {
    onrendered: function(canvas) {
       document.body.appendChild(canvas);
    }
});

#### 做个小例子代码如下，在线展示链接 <a href="https://github.com/Zylovehe/htmlToPdf/blob/master/demo01.html">demo1</a>


       