## html转成pdf，下载(html2canvas)

### html2canvas
### 简介
##### 我们可以直接在浏览器端使用html2canvas,对整个或局部页面进行‘截图’。但这并不是真的截图，而是通过遍历页面DOM结构，收集所有元素信息及相应样式，渲染出canvas image。

##### 由于html2canvas只能将它能处理的生成canvas image，因此渲染出来的结果并不是100%与原来一致。但它不需要服务器参与，整个图片都由客户端浏览器生成，使用很方便。

#### 使用

#### 使用的API也很简洁，下面代码可以将某个元素渲染成canvas：

html2canvas(element, {
    onrendered: function(canvas) {
        // canvas is the final rendered <canvas> element
    }
});

##### 通过onrendered方法，可以将生成的canvas进行回调，比如插入到页面中：

html2canvas(element, {
    onrendered: function(canvas) {
       document.body.appendChild(canvas);
    }
});

##### 做个小例子代码如下，在线展示链接 <a href="./demo01.html">demo1</a>

### 文字生成PDF

#### 使用方法如下：
// 默认a4大小，竖直方向，mm单位的PDF
var doc = new jsPDF();

// 添加文本‘Download PDF’
doc.text('Download PDF!', 10, 10);
doc.save('a4.pdf');

#### 参考demo02

### 图片生成PDF

#### 使用方法如下：

// 三个参数，第一个方向，第二个单位，第三个尺寸格式
var doc = new jsPDF('landscape','pt',[205, 115])

// 将图片转化为dataUrl
var imageData = ‘data:image/png;base64,iVBORw0KGgo...’;

doc.addImage(imageData, 'PNG', 0, 0, 205, 115);
doc.save('a4.pdf');

#### 参考demo03

### 文字与图片生成PDF

// 三个参数，第一个方向，第二个尺寸，第三个尺寸格式
var doc = new jsPDF('landscape','pt',[205, 155])

// 将图片转化为dataUrl
var imageData = ‘data:image/png;base64,iVBORw0KGgo...’;

//设置字体大小
doc.setFontSize(20);

//10,20这两参数控制文字距离左边，与上边的距离
doc.text('Stone', 10, 20);

// 0, 40, 控制文字距离左边，与上边的距离
doc.addImage(imageData, 'PNG', 0, 40, 205, 115);
doc.save('a4.pdf')

#### 参考demo04

### 单页

#### 将demo1的例子修改下：

<script type="text/javascript" src="./js/jsPdf.debug.js"></script>
<script type="text/javascript">
      var downPdf = document.getElementById("renderPdf");
      downPdf.onclick = function() {
          html2canvas(document.body, {
              onrendered:function(canvas) {

                  //返回图片dataURL，参数：图片格式和清晰度(0-1)
                  var pageData = canvas.toDataURL('image/jpeg', 1.0);

                  //方向默认竖直，尺寸ponits，格式a4[595.28,841.89]
                  var pdf = new jsPDF('', 'pt', 'a4');

                  //addImage后两个参数控制添加图片的尺寸，此处将页面高度按照a4纸宽高比列进行压缩
                  pdf.addImage(pageData, 'JPEG', 0, 0, 595.28, 592.28/canvas.width * canvas.height );

                  pdf.save('stone.pdf');

              }
          })
      }
</script>

#### 参考demo05


#### 如果页面内容根据a4比例转化后高度超过a4纸高度呢，生成的pdf会怎么样？会分页吗？
#### 可以尝试一下demo6

### 多页可以参考demo7

### 两边 留边距 参考demo8

#### 修改imgWidth，并且在addImage时x方向参数设置你要的边距，具体代码如下

var imgWidth = 555.28;
var imgHeight = 555.28/contentWidth * contentHeight;
...
pdf.addImage(pageData, 'JPEG', 20, 0, imgWidth, imgHeight );
...
pdf.addImage(pageData, 'JPEG', 20, position, imgWidth, imgHeight);

### 最后附上几个jsPDF的官方网址:

#### <a href="http://rawgit.com/MrRio/jsPDF/master/"> http://rawgit.com/MrRio/jsPDF/master/</a>

#### <a href="http://rawgit.com/MrRio/jsPDF/master/docs/index.html">http://rawgit.com/MrRio/jsPDF/master/docs/index.html</a>

#### <a href="http://mrrio.github.io/">http://mrrio.github.io/</a>
 
 

       