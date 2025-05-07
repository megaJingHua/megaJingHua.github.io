---
title: 相機調用、讀取input檔案、轉為base64、渲染相片、壓縮圖片、FormData送出
tags: [Javascript]
layout: single
date: 2020-03-04
toc: true
toc_sticky: true

---


## 📍Input file (相機調用)
``` xml
<from >
    <input type="file" name='img' id='input' accept="image/*" capture='camera'>
</from>
```
* accept：開啟系統檔案類型
    > camera–照相機；camcorder–攝像機；microphone–錄音
* capture：調用系統預設的裝置
:::warning
備註 :去除capture可同時調用相簿(Android不一定支援)
:::

###### 資料來源：[採集用戶的圖像](https://developers.google.com/web/fundamentals/media/capturing-images/?hl=zh-tw)、[H5頁面支援拍照選擇圖片](https://codertw.com/%E7%A8%8B%E5%BC%8F%E8%AA%9E%E8%A8%80/511036/)



## 📍FileReader (讀取input檔案)
``` Xml
<input type = "file" id = "file" name = "file" />
<div id = "result"> </div>
```
``` javascript
<script>
  function ProcessFile() { 
    var file = document.getElementById('file').files[0];//檔案位置
      var reader = new FileReader();//新FileReader事件
      reader.readAsDataURL( file );//readAsDataURL方法將檔案轉為base64
      reader.onload = function ( event ) { 
        var txt = event.target.result;//取得base64
        var img = document.createElement("img");//創建img
        img.src = txt;//將轉成base64的檔案塞入畫布
        document.getElementById("result").appendChild( img );
      };
    }
   
  function contentLoaded() {
    document.getElementById('file').addEventListener( 'change' ,
    ProcessFile);
  }

  window.addEventListener( "DOMContentLoaded" , contentLoaded);
</script>
```

能以非同步（asynchronously）方式讀取儲存在用戶端的檔案（或原始資料暫存）內容。
#### 瀏覽器相容性
![](https://i.imgur.com/4p77tfE.png)
![](https://i.imgur.com/KDgEufg.png)
#### 調用FileReader對象
![](https://i.imgur.com/Xup6yK9.png)
### readAsDataURL方法 (轉為base64)
:::warning
```
data:image/jpeg; base64, /9j/4AAQSkZJRgABAQAAAQABAAD/2wBDA
```
使用base-64進行編碼，由data開始 + MIME type + base64字符串(編碼過的內容)
:::

### target.result(取得URL渲染相片)
*  target：返回觸發事件的元素。
*  result：返回的數據格式取决于用哪種讀取方法来執行(只有在讀取操作完成后，此屬性才有效)。

###### 資料來源：[HTML5之FileReader的使用](https://blog.csdn.net/jackfrued/article/details/8967667)、[FileReader](https://developer.mozilla.org/zh-TW/docs/Web/API/FileReader)、[FileReader對象的readAsDataURL方法來讀取圖像文檔](https://hk.saowen.com/a/a80942f3c6f73e6fe85ac23eaeaa70fe19da0955f632320784007944d301ef5f)、[target Event Property](https://www.w3schools.com/jsref/event_target.asp)、[FileReader.result](https://developer.mozilla.org/en-US/docs/Web/API/FileReader/result)

## 📍Canvas (壓縮圖片)
:::success
因圖片檔案大小過大與手機效能過低導致無法傳送，所以將圖片壓縮或轉為 base64 傳輸。
:::
``` javascript
// base64圖片加載完畢後
var img = new Image();
var file = document.getElementById('image');
img.onload = function () {

    // 創建畫布(canvas)
    var canvas = document.createElement('CANVAS');
    var ctx = canvas.getContext('2d');
    
    // 圖片壓縮比例
    var tt = 200 / this.width;
    
    // canvas對圖片進行縮放
    canvas.height = this.height * tt;
    canvas.width = this.width * tt;
    
    // 圖片壓縮
    ctx.drawImage(this, 0, 0, canvas.width, canvas.height);
    
    // 回傳含有圖像和參數設置特定格式的 data URIs
    var dataURL = canvas.toDataURL("image/jpeg");
    
    // 將原始檔案替換為壓縮後檔案
    file.dataset.base64 = dataURL;
    
    // 清空畫布(canvas)
    canvas = null;
};
```

### toDataURL()
``` javascript
canvas.toDataURL(type, encoderOptions);
```
回傳含有圖像和參數設置特定格式 ( base 64 )的 dataURL 
* type：圖像格式，預設為 image/png。
* encoderOptions : 圖像品質為0到1之間的Number。

### drawImage()
在畫布上繪製圖像或視頻，也能重繪。
``` javascript
context.drawImage(img, sx, sy, swidth, sheight, x, y, width, height);
```
* img：繪製圖像、畫布或視頻。
* sx：開始剪裁的 x 座標位置。
* sy：開始剪裁的 y 座標位置。
* swidth：被剪切圖像的寬度。
* sheight：被剪切圖像的高度。
* x：在畫布上放置圖像的 x 座標位置。
* y：在畫布上放置圖像的 y 座標位置。
* width：圖像的寬度。（伸展或縮小圖像）
* height：圖像的高度。（伸展或縮小圖像）

###### 資料來源：[前端通過canvas實現圖片壓縮](https://hk.saowen.com/a/950ce49d30fc5d21cc10c2b4562554b0d32d3f5dfbd89f9fb236e3b234cbfe52)、[HTMLCanvasElement.toDataURL()](https://developer.mozilla.org/zh-TW/docs/Web/API/HTMLCanvasElement/toDataURL)、[HTML5 canvas drawImage() 方法](http://www.w3school.com.cn/html5/canvas_drawimage.asp)

## 📍FormData (送出資料)
FormData用以將數據編譯成鍵值對，以便用來發送數據。資料型態為Blob、File或者String(不是Blob也不是File，則會被轉為字串)。
``` xml
<form enctype="multipart/form-data" method="post" name="fileinfo"><!--表單名 name="fileinfo"-->
  <label>Your email address:</label>
  <input type="email" autocomplete="on" autofocus name="userid" placeholder="email" required size="32" maxlength="64" /><br /><!--資料名 name="userid"-->
  <label>Custom file label:</label>
  <input type="text" name="filelabel" size="12" maxlength="32" /><br /><!--資料名 name="filelabel"-->
  <label>File to stash:</label>
  <input type="file" name="file" required /><!--資料名 name="file"-->
  <input type="submit" value="Stash the file!" />
</form>
```
:::warning
```
fileninfo = {
    userid: 'email',
    filelabel: 'text',
    file: file
}
```
將資料取name，FormData會自動帶入。例子資料顯示如上。
:::
``` javascript
var formData = new FormData(document.forms.namedItem("fileinfo"));  // 建立表單
formData.append("CustomField", "This is some extra data");  // 附加資料
$.ajax({  //使用jQuery傳送formData
  url: "stash.php",
  type: "POST",
  data: formData,
  processData: false,  // 不處理數據
  contentType: false   // 不設置內容類型
});
```
#### append()方法
可直接向FormData對象附加File或Blob類型的文件

:::danger

``` javascript
processData: false,  // 不處理數據
contentType: false   // 不設置內容類型
```
使用jQuery傳送formData一定要設置processData、contentType
:::

###### 資料來源：[FormData 对象的使用](https://developer.mozilla.org/zh-CN/docs/Web/API/FormData/Using_FormData_Objects)
