# WebAssembly Barcode Reader
The web client-side barcode reader is built with **Dynamsoft WebAssembly Barcode SDK**. It is a pure HTML5 app without any server-side code.

### Get a Valid License
https://www.dynamsoft.com/CustomerPortal/Portal/Triallicense.aspx

## HowTo
Initialize parameters:

```javascript
var dynamsoft = self.dynamsoft || {};
var reader;
dynamsoft.dbrEnv = dynamsoft.dbrEnv || {};
dynamsoft.dbrEnv.resourcesPath = "https://tst.dynamsoft.com/demo/DBR_WASM";
dynamsoft.dbrEnv.licenseKey = "t0068NQAAAFEiYhAfkotGqCdX6THMV7KARQKp5h14F7LrM4LoGND9F5AdXykh+TOYHnBnMw80FMeKjMJbieYYos5dYLSn/Do=";
dynamsoft.dbrEnv.onAutoLoadWasmSuccess = function () {
  reader = new dynamsoft.BarcodeReader();
};
dynamsoft.dbrEnv.onAutoLoadWasmError = function (status) {
  
};
```

After configuring parameters, include `dynamsoft.barcodereader.min.js` at the bottom of your HTML page.

```html
<script src="https://tst.dynamsoft.com/demo/DBR_WASM/dynamsoft.barcodereader.min.js"></script>
```

### Read an image file

```javascript
let image = document.getElementById('uploadImage').files[0];
if (image) {
    reader.decodeFileInMemery(image).then(results => {
        let txts = [];
        for (let i = 0; i < results.length; ++i) {
            txts.push(results[i].BarcodeText);
        }
        barcode_result.textContent = txts.join(", ");
    });
}
```
### Read ArrayBuffer

```javascript
var imageData = barcodeContext.getImageData(0, 0, imageWidth, imageHeight);
var idd = imageData.data;
reader.decodeBuffer(idd.buffer, imageWidth, imageHeight, imageWidth * 4, dynamsoft.BarcodeReader.EnumImagePixelFormat.IPF_ARGB_8888).then(
    results => {
        let txts = [];
        for (var i = 0; i < results.length; ++i) {
            if (results[i].LocalizationResult.ExtendedResultArray[0].Confidence >= 30) {
                txts.push(results[i].BarcodeText);
            }
        }
    }
);
```

![webassembly barcode reader in Chrome](https://www.codepool.biz/wp-content/uploads/2018/07/webassembly-barcode-dynamsoft.gif)

## Blog
[The Preview of Dynamsoft WebAssembly Barcode SDK](https://www.codepool.biz/javascript-webassembly-barcode-sdk.html)
