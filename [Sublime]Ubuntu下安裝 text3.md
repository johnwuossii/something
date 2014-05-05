##[Sublime]Ubuntu下安裝 text3

#### Ubuntu Linux 下安裝用` PPA `

安裝 Sublime Text 3：

    sudo add-apt-repository ppa:webupd8team/sublime-text-3
    sudo apt-get update
    sudo apt-get install sublime-text-installer

####設定terminal的sublime3

    vim ~/.bashrc
    
然後在最下面加入以下兩行

    # set sublime3
    alias sublime3='/opt/sublime_text/sublime_text'

####調整字型和佈景

Monaco 在 Mac OS X 系統是內建的字型，但是到 Linux 與 Windows 則必須另外安裝，字型檔可以從這個 GitHub 的專案取得：https://github.com/todylu/monaco.ttf

Sublime Text 的字型與佈景設定範本如下。

```js
{
 "color_scheme": "Packages/Color Scheme - Default/Solarized (Dark).tmTheme",
 "font_size": 11,
 "font_face": "Monaco"
}
```

Solarized 是一套講究準確用色的佈景，個人相當推薦。

##參考網址

http://blog.lyhdev.com/2013/10/sublime-text-2-ubuntu-linux-package.html
