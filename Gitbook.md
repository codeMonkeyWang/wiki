## Gitbook

* 安装 gitbook    

> gitbook 2.0版之后开始使用下面的命令安装，`npm install gitbook -g` 为旧版本

`$ npm install gitbook-cli -g` 

* 本地预览
 
`gitbook serve`

* 输出静态网站

`$ gitbook build ./repository --output=./outputFolder`

* 帮助
`gitbook help`


## 错误处理
**Error: Need to install ebook-convert from Calibre**

<http://calibre-ebook.com/>

Calibre 上下载calibre-2.17.0.dmg,之后安装，选择英文版（方便找到calibre - Preferences - Miscellaneous - Install command line tools），找不到Install command line tools则可以终端执行 ：

`ln -s /Applications/calibre.app/Contents/MacOS/ebook-convert /usr/local/bin `