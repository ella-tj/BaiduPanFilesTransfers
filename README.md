# 软件介绍

百度网盘批量转存软件，基于 `Python 3.10` + `Tkinter` 构建。可用于批量转存网络上分享的百度网盘链接到自己的百度网盘上。

介绍页面请访问：[小众软件](https://meta.appinn.net/t/topic/16995/39)

软件最新版截图：

![百度网盘批量转存软件 2.0 版本截图](https://raw.githubusercontent.com/hxz393/BaiduPanFilesTransfers/master/Capture/%E6%88%AA%E5%9B%BE2.0.jpg)

## 下载地址

软件开发编译环境为 `Win10 x64` 专业版，版本号 `22H2`。只要是 `Win10` 64 位操作系统的用户可以直接下载打开使用。

其他操作系统理论上可以手动编译成可执行文件，编译流程参见下面自行打包小节。

软件下载方式：

- 方式一：到 [release](https://github.com/hxz393/BaiduPanFilesTransfers/releases) 页面下载最新版的 `exe` 文件，文件名类似 `BPFTv2.0.exe`，下载完毕可直接打开使用。
- 方式二：百度网盘分流下载地址：https://pan.baidu.com/s/1h445UmgNNFFIPO0elmVfgQ?pwd=2i9j
- 方式三：百度网盘秒传链接：7013f39c3bdcba349ef59bd67aa0286b#13786282#BPFTv2.1.zip



## 自行打包

手动编译需要事先安装好 `Python 3.6` 以上版本，和 `pyinstaller` 软件包。其他依赖报缺啥装啥，安装方式请自行搜索网络。

编译步骤如下：

1. 在安装有 `Git` 的主机上克隆项目。命令如下：

   ```sh
   git clone https://github.com/hxz393/BaiduPanFilesTransfers.git
   ```

   或者在 [项目主页](https://github.com/hxz393/BaiduPanFilesTransfers) 点击绿色`<> Code` 按钮选择 `Download ZIP` 选项，[下载](https://github.com/hxz393/BaiduPanFilesTransfers/archive/refs/heads/master.zip) 源码压缩包。下载完毕后用压缩软件或命令工具解压缩。

2. 使用命令切换到项目路径下面。

   例如在 Windows 系统下面，打开 `CMD` 命令提示符，输入：

   ```sh
   cd B:\2.脚本\BaiduPanFilesTransfers
   B:
   ```

   在 Linux 系统下面，通用使用 `cd` 命令切换到项目路径下面：

   ```sh
   cd /root/BaiduPanFilesTransfers
   ```

3. 使用 `pyinstaller` 命令编译打包成可执行文件：

   ```sh
   pyinstaller -F -w -i bpftUI.ico bpftUI.py
   ```

   如果过程没有报错，可执行文件会生成到 `dist` 目录下面。



## 版本说明

软件重构后的 2.X 版本已发布，没经过充分测试，可能有无法预料的 BUG，欢迎提交 [Issue](https://github.com/hxz393/BaiduPanFilesTransfers/issues) 反馈。同时 1.13 版本依然可用（截至 2023.05.12），但后续不再更新 1.X 版本。



## 开源许可

本软件采用 [GPL-3.0 license](https://github.com/hxz393/BaiduPanFilesTransfers/blob/master/LICENSE) 源授权许可协议，若违背开源社区的基本准则，将开源项目据为私有用于商业用途，属于侵权行为，本人将追究法律责任。



# 软件使用

软件使用分为下面几个步骤。

## 获取 Cookies

使用 `Chrome` 或类似浏览器访问[百度网盘主页](https://pan.baidu.com/)，完全载入后按 `F12` 键调出控制台。选择 `网络（NetWork） `选项卡。

如下图所示，目前应该空空如也：
![向导图1](https://raw.githubusercontent.com/hxz393/BaiduPanFilesTransfers/master/Capture/u-1.png)
按 `F5` 刷新页面，下面出现很多条记录。单击名为 `main` 开头的记录，右边会出现菜单，显示标头（Headers）、响应（Response)等内容。

在标头页面往下翻，找到请求标头中以 `Cookie:` 开头的行，后面有一串以 `XF` 开头的内容，这就是需要找的 `Cookies`。把它们全部选中，右键选择复制，粘贴到软件对应输入框内。如下图所示：
![向导图2](https://raw.githubusercontent.com/hxz393/BaiduPanFilesTransfers/master/Capture/u-2.png)



## 获取 User-Agent（1.x 版本）

只有 1.x 版本需要手动填入 `User-Agent`。

接上操作往下下翻到最底部，能看到 `User-Agent` 项目。同样把它复制粘贴到软件对应输入框便行了。软件会自动保存当前配置，下次无需重复获取。示例图如下：
![向导图3](https://raw.githubusercontent.com/hxz393/BaiduPanFilesTransfers/master/Capture/u-3.png)



## 输入保存位置

保存位置如果留空不填，文件会保存到根目录下，也就是打开百度网盘主页便能看到。

输入文件保存位置后，如果目录不存在，会自动新建目录。如果目录已存在，则直接转存在指定目录下。

保存位置（目录）不能包含大多数英文特殊符号，例如：`>`、`|`、`*`、`?`、`:`、`/` 等。如果输入的特殊符号不被允许，软件会检测到并中断运行。

如果保存路径加文件名一起长度超过 255 个字符，用百度网盘客户端下载文件时会失败。应尽量使用有意义的英文加数字作为保存目录名。



## 输入网盘链接

软件已经尽可能地适配常见百度网盘链接格式。如果软件运行时提示 ”不支持的链接“，请检查输入链接是否符合下面格式规范。

**标准链接：**

```sh
https://pan.baidu.com/s/1nvBwS25lENYceUu3OMH4tg 6img
https://pan.baidu.com/s/1nvBwS25lENYceUu3OMH4tg?pwd=6img
https://pan.baidu.com/s/1nvBwS25lENYceUu3OMH4tg 提取码：6img
https://pan.baidu.com/s/1nvBwS25lENYceUu3OMH4tg 提取:6img
https://pan.baidu.com/s/1EFCrmlh0rhnWy8pi9uhkyA
https://pan.baidu.com/share/init?surl=W7U9g47xiDez_5ItgNIs0w
```

**游侠 v1 标准：**

```sh
https://pan.baidu.com/#bdlink=QkQyMTUxNjJENzE5NDc4QkNBRDJGMTMyNTlFMTEzNzAjRkJBMTEzQTY1M0QxN0Q1NjM3QUQ1MEEzRTgwMkE2QTIjMzcxOTgxOTIzI1pha3VybyAyMDAxMjYuN3oK
bdlink=QkQyMTUxNjJENzE5NDc4QkNBRDJGMTMyNTlFMTEzNzAjRkJBMTEzQTY1M0QxN0Q1NjM3QUQ1MEEzRTgwMkE2QTIjMzcxOTgxOTIzI1pha3VybyAyMDAxMjYuN3oK
```

**梦姬标准：**

```sh
965FEAFCC6DC216CB56128B531694C9D#495B4FB5879AE0B22A31826D33D86D80#802846691#梦姬标准.7z
4159f28726f88ba7aab8cbb6a8afbae1#201442718#patch.rar
```

**Go 格式：**

```sh
BaiduPCS-Go rapidupload -length=418024594 -md5=31f141fee63d038a46db179367315f3a -slicemd5=5b2c842f421143a9a49938dc157c52e6 -crc32=3179342807 \"/音乐/Yes/1969. Yes.zip\"
```

**PanDL 标准：**

```sh
bdpan://44K344Or44Kv44Gu5p6c5a6fICsg44Go44KJ44Gu44GC44Gq44CA5o+P44GN5LiL44KN44GXOFDlsI/lhorlrZAg5pel5paHLnppcHw2NDAxODQxNTd8ZDNjOTBmOTI3ZjUxYzIyMmRjMTc1NDM1YTY0OWMyYTJ8OTk4NTE0NDE3Y2I5Y2I0MTQ0MGRlZTFiMmMyNTYwMzY=`
```



## 执行转存

所有信息输入完毕后，点击运行按钮来执行批量转存百度网盘链接。

转存执行时没有暂停功能，可以直接点击软件窗口右上角关闭软件来终止运行。



## 使用系统代理

软件默认会绕过网络系统代理，但不能绕过网络全局代理。

如果处于特殊网络环境下，需要配置网络系统代理模式，才能正常访问百度网盘，勾选上 “使用系统代理” 勾选框后，再执行转存。



# 常见问题

使用软件遇见错误时，先查看下面总结的一些常见问题和解决方案。再查看所有 [Issue](https://github.com/hxz393/BaiduPanFilesTransfers/issues) 中是否有同样问题。如果都没有帮助，再提交 [Issue](https://github.com/hxz393/BaiduPanFilesTransfers/issues) ，我一般当天或隔天会回复。

## 转存失败，错误代码 XX

如果软件突然不能使用。

**原因**：Cookie 失效或不正确。百度网盘改版，软件失效。

**解决**：先试着通过浏览器无痕模式打开百度网盘主页，登陆获取的 Cookie 看能不能正常工作。如果换了多台电脑和账号都不工作，那就是软件需要修复更新了。可以提交 [Issue](https://github.com/hxz393/BaiduPanFilesTransfers/issues) 反馈。



## 只有第一个链接转存成功

后面链接提示 “链接错误尝试次数过多”。

**原因**：Cookie 不正确。

**解决**：通过浏览器无痕模式打开百度网盘主页，重新登陆获取 Cookie 即可。



## 链接错误尝试次数过多

**原因**：通常见于带提取码的链接。如果短时间内对着一个链接反复转存 3 次以上，不管提取码是否正确，都会触发百度网盘防御机制。如果直接在网页端访问链接，会发现要输入验证码。

**解决**：只影响单个链接，其他链接能够正常转存。可以手动转存个别问题链接。如果所有链接都报这一错误，参考问题 “只有第一个链接转存成功” 的解决办法。



## 转存次数到达 1000 上限

连续转存 1000 个链接，再多 1 个都会报错。报错码千奇百怪。甚至网页端都无法再转存，提示 “数据错误,请稍后重试” 。

**原因**：百度网盘基于 IP 地址层面的封锁，禁止用户大量转存。

**解决**：可以重启拨号路由器，更换对外 IP 地址。如果需要使用代理服务器，可以修改源码，注释掉 `self.session.trust_env = False` 这行代码。



## 免费用户转存 500 文件限制

**原因**：一般常见于文件夹转存，免费用户被百度限制，文件夹内文件数超过 500 个，会提示 “转存文件数超过限制”。

**解决**：暂时不打算支持，除非哪天软件改为调用百度网盘 API 接口的工作方式，否则效率太低。而且一般 API 接口都有请求速率限制，API Key 或 token 也不好弄。有需要可以留一下其他开源或免费项目，或者开通百度网盘会员来解除限制。



## 百度群组文件转存

暂时不支持转存群组文件。群组文件共享功能用的人少，以后有需要再提供支持。



## 系统版本过低

一些 `Win 10` 以下的操作系统，运行时提示缺少必要 `dll` 文件。

**原因**：操作系统太旧，无法支持 `Python 3.10` 。

**解决**：升级系统，或者参考 “自行打包” 方法。



## 已有同名文件或文件夹存在

有时明明转存成功后，提示却是 “转存失败，目录中已有同名文件或文件夹存在”。

**原因**：触发机制不明。多见于秒传链接。

**解决**：最好在网页端确认下，是虚报，还是真有同名但实际上不同的文件。视情况手动处理。

 



# 更新日志
为避免更新日志过长，只保留最近更新日志。

## 版本 2.1（2023.05.16）

更新内容：

1. 添加 “使用系统代理” 勾选框。

修复内容：

1. 修复因为删除 `User-Agent` 参数，导致读取配置文件出错，打开软件报错。
2. 修改部分变量和函数名，使代码更规范。



## 版本 2.0（2023.05.12）

更新内容：

1. 调整程序 UI，支持随意调整窗口大小。

修复内容：

1. 改正错误的文本格式和标点符号。
2. 优化代码，重新封装函数。




## 版本 1.13（2023.03.21）

更新内容：

1. 添加程序运行图标。

修复内容：

1. 更换秒传转存请求接口，解决报错误代码 `9019` 问题;



## 版本 1.12.1（2023.01.08）

修复内容：

1. 修复秒传目录或文件名带 `&` 时触发 BUG。



## 版本 1.12（2023.01.03）

修复内容：

1. 更换秒传转存请求接口。
2. 修改部分秒传出错提示文字。
