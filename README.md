前端图片压缩
===

用于解决移动端上传图片过大的问题

```js
$("#imgFile").on("change", function(){
    /**
    * file 原始图片路径
    * cb 成功回调
    * quality 压缩质量，数值越小压缩程度越大
    */

    $.minifyImgUploade(this.files[0], function (imgData) {
        $("#modified").attr("src", imgData)
        // 通过base64实现压缩后图片的异步上传
        // $.post("server.php", { imgData: imgData }, function (res) {
        //     console.log(1);
        // }, 'json');
    }, 0.2)
})
```

```php
// server.php

$imgData = $_REQUEST['imgData'];
$base64 = explode(',', $imgData)[1];
$img = base64_decode($base64);
$url = './test.jpg';
if (file_put_contents($url, $img)) {
    exit(json_encode(array(
        url => $url
    )));
}

```