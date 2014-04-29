##AngularJS-with-Django(衝突的{{}}標籤)

Q: 我想要用 AngularJS 搭配 Django, 但是他們都同要會用到 ` {{ }} ` 的模板標籤... 

有沒有什麼方法可以來改變其中一個的模板標籤？

A: 使用 `$interpolateProvider`來改變 AngularJS 的標籤:

  http://docs.angularjs.org/api/ng.$interpolateProvider
  
  ```javascript
  myModule.config(function($interpolateProvider) {
    $interpolateProvider.startSymbol('{[{');
    $interpolateProvider.endSymbol('}]}');
  });
  ```
  
##參考網址

http://stackoverflow.com/questions/8302928/angularjs-with-django-conflicting-template-tags
