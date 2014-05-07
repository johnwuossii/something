##[mongo]開啟使用者認證功能(Authentication)

第一步，建立一個最高權限帳號，請用在 MongoDB Shell 執行下面這二行的指令

```bash
use admin
db.addUser("root","12345678")
```
第二步，請把 MongoDB 給 Shutdown 後，再用下面的指令來啟動  MongoDB，如果沒有加上 "—auth” 這個參數

※這是啟動驗證功能之意，如果沒有此參數就啟動Mongod，那即使設定了帳戶，也沒有效果
```bash
$ sudo stop mongodb
$ mongod --auth
$ sudo start mongodb
```

MongoDB 啟動完成之後，再用 Robomongo 做查詢和修改。

P.S.沒有裝的朋友請用`$ sudo apt-get install robomongo`

Robomongo Create 設定：

    Connection>
    Address: locahost : 27017
    
    Authentication>
    Perform authentication 打勾
    User Name: root
    Password: 12345678

###榜定ip讓外部呼叫

```bash
$ vim /etc/mongodb.conf
```
將 `bind_ip = 127.0.0.1` 改成 `bind_ip = '自己的ip'`

最後記得重啟  
```bash
$ sudo restart mongodb
```
nodejs如果要連mongo的url寫法：

    mongodb://[username:password@]host1[:port1][,host2[:port2],...[,hostN[:portN]]][/[database][?options]]


##出處

http://blog.xuite.net/zack_pan/blog/67722231-%E7%AC%AC%E4%B8%80%E6%AC%A1%E7%94%A8mongodb

http://mongodb.github.io/node-mongodb-native/driver-articles/mongoclient.html#the-url-connection-format
