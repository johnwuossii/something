##[NodeJs]圖片浮水印

裝`gm`就不多說了
```
npm install gm
```

DEMO CODE

```js
var gm = require('gm');

gm('/path/to/image.jpg')
  .resize(353, 257)
  .autoOrient()
  .font('w9.ttf')
  .fontSize(36)
  .drawText(30, 35, '幹你娘還要下載字型檔')
  .write('./output/output.jpg', function(err){
    if(err){
      console.dir(err);
      process.exit();
    }
    console.dir('Success, image in ./output/output.jpg');
    process.exit();
  });
```

記得安裝軟體跟字型 謝謝！

##參考網址

http://codelife.me/blog/2012/09/20/create-warkmarked-picture-using-node-js/
http://aheckmann.github.io/gm/
