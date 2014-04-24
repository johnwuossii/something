#lxde/Lubuntu 的快捷鍵


###註釋

`縮寫字母`  |  鍵名

---------------------------

  ` C `   |  Ctrl   鍵               
  
  ` A `   |  Alt    鍵
  
  ` W `   |  Window 鍵   

###快捷鍵列表

  ` 快捷鍵  `    |      功能說明

---------------------------

  `C-A-Left `      切換到左面桌面

  `C-A-Right `     切換到右面桌面

  `SA-Left   `     將窗口發送到左面桌面，同時也切換到左面桌面

 ` SA-Right  `     將窗口發送到右面桌面，同時也切換到右面桌面

  `W-F1      `     切換到1號桌面

  `W-F2      `     切換到2號桌面

  `W-d       `     顯示底桌面

  `A-F4      `     關閉視窗

  `A-space   `     視窗menu

  `A-Tab     `     下一個視窗

  `A-S-Tab   `     上一個視窗

  `W-e       `     文件總管PCManFM

 ` W-r       `     啟動gmrun運行管理器

 ` A-F2      `     啟動gmrun運行管理器

 ` C-Escape  `     啟動menu

  `F11       `     全螢幕顯示

  `A-C-Delete  `   啟動lxtask任務管理器
  
###自訂快捷鍵
  
  快捷鍵是通過openbox來實現的，在~/.config/openbox 目錄下有一個lxde-rc.xml文件，
  其中有類似如下格式就是設置快捷方式。
  同時也可以看到系統默認已經設置了快捷方式。

```HTML
<!-​​- Keybindings for running applications -->
<keybind key="W-e">
<action name="Execute">
<startupnotify>
<enabled>true</enabled>
<name>PCManFM</name>
</startupnotify>
<command>pcmanfm</command>
</action>
```
