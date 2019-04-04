# pdf-to-image

# 要想实现这个场景功能需要解决以下几个问题：

1. 用户上传文档后，怎么将文档展示在页面供用户浏览！

2. 是否可以直接利用JS在前端完成，这样省去了后端处理，提供URL再让用户下载的麻烦！

3. 假如直接利用JS实现该功能，处于安全策略，JS是不能直接打开本地文件！


## 实现：

# 针对问题1：用户上传文档后，怎么将文档展示在页面供用户浏览！

(1)、如果是单纯的PDF文档展示在网页中，我们可以利用HTML的标签，并且效果也不错。

(2)、但是我们这里需要的是将PDF转化成图片或者canvas，这就不得不说PDF.js了，PDF.js可以将PDF文档转换成canvas实现预览，有了canvas，我们就有了图片。其中这个JS框架使用起来也很简单，前往项目官网下载主要的pdf.js文件，并将其引入项目，具体的使用方法可自行百度、Google.

# 针对问题2：在实现问题1的基础上，批量下载图片！

(1)、如果只是单个下载图片，比如下载一张图片，可通过如下代码实现（利用<a>标签的相关属性）

    var a = $("<a>").attr("href", "http://***").attr("download", "img.png").appendTo("body");


(2)、如果要支持批量下载图片，可使用jszip.js实现多张图片添加到压缩文件供下载，使用FileSaver.js实现压缩文件的保存、下载！其中需要注意的是jszip下载的数据流为blob，可使用如下方法将dataUrl转换为blob，FileSaver.js也提供了相应的函数功能，这里使用在百度上找的一段代码。
    //dataURL转成Blob
    function dataURLtoBlob(dataurl) {
        var arr = dataurl.split(','),
        mime = arr[0].match(/:(.*?);/)[1],
        bstr = atob(arr[1]),
        n = bstr.length,
        u8arr = new Uint8Array(n);
        while(n--) {
            u8arr[n] = bstr.charCodeAt(n);
        }
        return new Blob([u8arr], {type: mime});
    }

# 针对问题3：JS如何打开本地文件！

出于安全策略，JS不能随意操作文件，可利用FileReader实现本地文件的打开，具体的实现方法可自行搜索或参考项目中的解决方案。

传送门：https://xxlllq.github.io