
#failed to connect to localhost 27017

這個問題可以通過下面4個步驟來解決

1)  刪除 .lock 檔案

    $ sudo rm /var/lib/mongodb/mongod.lock 

2)  修復 mongodb

    $ mongod –repair

3)  啟動 mongodb

    $ sudo service mongodb start 

4)  start the mongo client

    $ mongo

欲了解更多詳細信息 http://shakthydoss.com/error-couldnt-connect-to-server-127-0-0-127017-srcmongoshellmongo-js-exception-connect-failed/
