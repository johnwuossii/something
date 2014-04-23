#Error: couldn’t connect to server 127.0.0.1:27017 src/mongo/shell/mongo.js: exception: connect failed

這個問題可以通過下面4個步驟來解決

1)  刪除 .lock 檔案

    $ sudo rm /var/lib/mongodb/mongod.lock 

2)  修復 mongodb

    $ mongod –repair

3)  啟動 mongodb

    sudo start mongodb

4) 檢查 mongodb 狀態 

    sudo service mongodb status 

(or)

    sudo status mongodb

5)  啟動 mongo client

    $ mongo

欲了解更多詳細信息 http://shakthydoss.com/error-couldnt-connect-to-server-127-0-0-127017-srcmongoshellmongo-js-exception-connect-failed/
