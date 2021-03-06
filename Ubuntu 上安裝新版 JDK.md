##Ubuntu 上安裝新版 JDK
**Step1**

首先到Oracle官網上下載，最新版的`"jdk-7u25-linux-x64.tar.gz"` or `"jdk-7u25-linux-i586.tar.gz"`

(事先建立一個Downloads的資料夾，下載的東西都可放這裡面集中。)
 
**Step2**

將下載下來的JDK檔進行解壓縮，指令：`tar -zxvf jdk-7u25-linux-i586.tar.gz`
 
**Step3**

複製解壓縮後的資料夾`jdk_1.7.0_25`，到`/usr/lib/jdk/`目錄下面，指令`：cp -r ~/Downloads/jdk1.7.0_25/ /usr/lib/jdk/`

(這裡如果沒有jdk資料夾，則建立該資料夾，指令：`sudo mkdir /usr/lib/jdk`)
 
**Step4**

設置環境變數，打開文件/etc/profile，指令：`sudo vi /etc/profile`
 
**Step5**

在文件的最後端加上：
```bash
export JAVA_HOME=/usr/lib/jdk/jdk1.7.0_25 
export JRE_HOME=/usr/lib/jdk/jdk1.7.0_25/jre 
export PATH=$JAVA_HOME/bin:$JAVA_HOME/jre/bin:$PATH
export CLASSPATH=$CLASSPATH:.:$JAVA_HOME/lib:$JAVA_HOME/jre/lib
```
**Step6**  

將系統默認的jdk修改過來，也就是java和javac指令由系統自帶的換成你自己安裝的
 
指令：
```bash
sudo update-alternatives --install /usr/bin/java java /usr/lib/jdk1.7.0_25/bin/java 300
sudo update-alternatives --install /usr/bin/javac javac /usr/lib/jdk1.7.0_25/bin/javac 300
sudo update-alternatives --config java
sudo update-alternatives --config javac
```
**Step7**

檢查版本，指令：`java -version`

如果出現以下字樣，代表順利完成安裝。
 
          java version "1.7.0_25"
          Java(TM) SE Runtime Environment (build 1.7.0_25-b15)
          Java HotSpot(TM) Server VM (build 23.25-b01, mixed mode)
