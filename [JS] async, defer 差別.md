##[JS] async, defer 差別
HTML5 `<script>` 多了屬性 async  和 defer 

###一般情況

``` html
<script src="demo.js" ></script>
```

整個網頁的繪製會停下，等 'demo.js' 下載完並執行完，網頁繪製才繼續。

###defer

```html
<script src="demo.js" defer ></script>
```
網頁繪製不會停下， 'demo.js' 在背景下載，待 DOMContentLoaded 再執行 `demo.js` 。

###async

```html
<script src="demo.js" async ></script>
```
網頁繪製不會停下， `demo.js` 在背景下載。

待 demo.js 下載完畢，網頁繪製停下，執行 demo.js 。

待 demo.js 執行完畢，網頁繪製繼續。

------------------------

Peter Beverloo 畫了張時序圖可供參考。

![時序圖](http://peter.sh/wp-content/uploads/2010/09/execution2.jpg)

------------------------

##引用網址

http://blog.xuite.net/vexed/tech/61308318-script+tag+%E5%B1%AC%E6%80%A7+async+defer+%E5%B7%AE%E5%88%A5

http://peter.sh/experiments/asynchronous-and-deferred-javascript-execution-explained/
