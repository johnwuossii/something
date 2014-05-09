##[NodeJs]圖片浮水印

```js
var spawn = require('child_process').spawn;

var composite = spawn('gm',
  [
      'composite',
      '-gravity',
      'SouthEast', //右下角
      '-dissolve',
      '80', //溶解度,和透明度类似
      'watermark.png',
      'src.jpg',
      'dest.jpg'
  ]);

composite.stdout.on('data',function(data){
  console.log(data);
});

composite.stderr.on('data',function(data){
  console.log(data);
});

composite.on('exit',function(code){
  if(code != 0){
      console.log('gm composite process exited with code ' + code);
  }
});
```

##轉載文章

http://codelife.me/blog/2012/09/20/create-warkmarked-picture-using-node-js/
