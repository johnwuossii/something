##[ubuntu]如何將apt-get來源伺服器換到美國

用 apt-get 更新套件清單 ( apt-get update ) 或是安裝軟體 (apt-get install ) 的時候，有時會發生連不到伺服器而無法下載套件的問題
,為了解決這樣的問題,這邊提供一個簡單的方法,把伺服器從台灣 Mirror 換至美國,詳細如下：

**1. 備份 sources.list**

開始之前，請記得先用下面的指令來做個備份，以防萬一哩 !

```bash
sudo cp /etc/apt/sources.list /etc/apt/sources.list.BAK 
```

**2.打開 sources.list** 

再來，就用 vim 來開啟記錄套件儲存庫清單的 sources.list 檔案。

```bash
sudo vi /etc/apt/sources.list 
```
**3.變更成其他國家的伺服器**

然後，在 vim 裡面，用下面這一行指令來把 tw 全部換成 us (全都是小寫的)。

```bash
:1,$s/tw/us/g 
```
**4.儲存  source.list**

完成變更後，用下面指令儲存檔案並離開 vim。
```bash
:wq 
```
**5.更新套件清單**

最後，要更新一下套件清單。
```bash
sudo apt-get update 
```
大功告成 !

###參考網址

http://iosdevelopersnote.blogspot.tw/2012/09/socketio.html
