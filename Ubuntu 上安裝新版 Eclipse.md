  #Ubuntu 上安裝新版 Eclipse
  
  首先，我們先到 Eclipse 官方網站上面下載最新版本的 Eclipse for Linux ，並且利用以下指令將它放到/opt/目錄下。
  
  http://www.eclipse.org/downloads/
  
  ```bash
    # X.X.X = 你下載的版本號
    $ sudo mv eclipse-SDK-X.X.X-linux-gtk.tar.gz /opt/
  ```
  
  然後解壓縮
```bash
    $ cd /opt/
    $ sudo tar -zxfv eclipse-SDK-X.X.X-linux-gtk.tar.gz
```
  再刪除tar檔
```bash  
    $ sudo rm eclipse-SDK-X.X.X-linux-gtk.tar.gz
```
  設定捷徑，要先開一個新的檔案，叫做 eclipse.desktop
```bash
    $ sudo vim /usr/share/applications/eclipse.desktop
```
  然後把以下資訊貼上
```bash
    [Desktop Entry]
    Name=Eclipse
    Type=Application
    Exec=/opt/eclipse/eclipse
    Terminal=false
    Icon=/opt/eclipse/icon.xpm
    Comment=Integrated Development Environment
    NoDisplay=false
    Categories=Development;IDE
    Name[en]=Eclipse
```
最後，把 eclipse.desktop 這檔案放到你的啟動列裡面就可以囉。

##例外處理

假如出現以下錯誤：

```bash
  A Java Runtime Environment (JRE) or Java Development Kit (JDK) 
  must be available in order to run Eclipse. No Java virtual machine 
  was found after searching the following locations: 
  /home/gaoyl/setup/eclipse/jre/bin/java 
  java in your current PATH
```
  如果通過終端，及以命令行的方式執行，則不會有問題，可以正常啟動。
  
  那請開終端做以下事情：
```bash
  $ cd <eclipse dir> 
  $ ln -sf $JRE_HOME jre
```
  目的是在eclipse安裝目錄下建立一個名稱為jre的鏈接，將其指向java安裝目錄下的jre目錄。
