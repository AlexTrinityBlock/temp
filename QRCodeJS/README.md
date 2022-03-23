# QR code掃描函數庫研究

這是給嘉義大學-洪燕竹老師課程的課後學習內容。

# Javascript函數庫

函數庫採用

## Html5-QRCode

[https://github.com/mebjas/html5-qrcode](https://github.com/mebjas/html5-qrcode)

## HTML程式

```html
<html>

<head>
    <title>Html-Qrcode Demo</title>

<body>
    <div id="qr-reader" style="width:500px"></div>
    <div id="qr-reader-results"></div>
</body>

<script src="./html5-qrcode.min.js"></script>

<script>
    document.addEventListener("DOMContentLoaded", function () {

        //以取得id="qr-reader-results"的HTML元素控制權
        var resultContainer = document.getElementById('qr-reader-results');
        //掃描結果計數器與一開始的掃描結果設置初始值為0
        var lastResult;
        var countResults = 0;

        var html5QrcodeScanner = new Html5QrcodeScanner(
            "qr-reader", { fps: 10, qrbox: 250 });

        function onScanSuccess(decodedText, decodedResult) {

            //如果掃描到的結果字串，跟上次掃描到的不一樣，則將內容加入HTML中。
            //這個避免了同一個QR code瞬間掃描了好幾次。
            if (decodedText !== lastResult) {

                //掃描結果文字計數器。
                ++countResults;

                //儲存掃描結果到變數
                lastResult = decodedText;

                //在開發者模式印出掃描結果，decodedText是指QR code的文字，而decodedResult則是Json格式的輸出。
                console.log(`Scan result = ${decodedText}`, decodedResult);

                //將新的掃描結果加入HTML中。
                resultContainer.innerHTML += `<div>[第${countResults}個掃描結果] - ${decodedText}</div>`;

                // 如果解開註解，當掃描成功時，就會刪除掉掃描框。
                // html5QrcodeScanner.clear();
            }
        }

        function onScanError(qrCodeError) {
            //這是可以放，當掃描失敗時的反應
        }

        //畫出掃描視窗，並且將成功與失敗的結果放入行動中。
        html5QrcodeScanner.render(onScanSuccess, onScanError);
    });
</script>
</head>

</html>
```

```javascript

```

