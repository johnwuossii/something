#[mongo]如何開啟使用者認證功能使用者認證功能(Authentication)

第一步，建立一個最高權限帳號，請用在 MongoDB Shell 執行下面這二行的指令

```bash
use admin
db.addUser("root","12345678")
```
第二步，請把 MongoDB 給 Shutdown 後，再用下面的指令來啟動  MongoDB，如果沒有加上 "—auth” 這個參數

```bash
$ sudo stop mongodb
$ mongod --auth
$ sudo start mongodb
```

MongoDB 啟動完成之後，再用 Robomongo 做查詢和修改。

P.S.沒有裝的朋友請用`$ sudo apt-get install robomongo`

Robomongo 設定：

    Connection>
    Address: locahost : 27017
    
    Authentication>
    Perform authentication 打勾
    User Name: root
    Password: 12345678



