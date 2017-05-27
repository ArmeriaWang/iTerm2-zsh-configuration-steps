## iTerm2和zsh安装/简单配置指南

小白向，更多个人配置文件待更新。



### 前期准备

由于系统默认的环境变量目录`/usr/bin/`在OS X 10.11之后取消了用户的写入权限，所以**将`/usr/local/bin/`加入环境变量**，方便之后操作。
``` bash
#用Terminal::vim打开.bash_profile，后按E进入赛艇模式
$ sudo vi ~/.bash_profile

#在文件末尾加入
export PATH="/usr/local/bin:$PATH"

#按esc，键入:wq!（强制保存并退出），回到bash

#使修改立即生效
$ source ~/.bash_profile
```


**安装Homebrew**。（来自 brew.sh）

``` bash
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

**安装iTerm2，wget，git**。
``` bash
$ brew cask install iterm2
$ brew install wget
$ brew install git

#可通过如下命令检查安装列表
$ brew list
```



### 配置iTerm2

安装好iTerm2后，就可以用它完全替代系统自带的Terminal。接下来配置iTerm2。

打开iTerm2，按组合键`⌘,`打开偏好设置。

- 全局热键显/隐iTerm2：

　　进入`Keys`选项卡，在`Hotkey`中勾选`Show/hide … system-wide key`，并设置快捷键。另可勾选`Hotkey toggles a dedicated window with profile `，让iTerm界面从屏幕上方折下来（颜色需另配置）。

- 字体设置：

　　为了最终不出现乱码，推荐安装[Menlo-Powerline](https://gist.github.com/qrush/1595572/raw/417a3fa36e35ca91d6d23ac961071094c26e5fad/Menlo-Powerline.otf)或[Monaco-Powerline](https://github.com/mneorr/powerline-fonts/blob/bfcb152306902c09b62be6e4a5eec7763e46d62d/Monaco/Monaco%20for%20Powerline.otf)，之后在`Profiles`→`Text`→`Change Font`中更换iTerm2的显示字体。


- 颜色配置：

  若对预设配置方案不满意又不愿意倒腾，可直接从git下载Solarized主题（默认下载目录是 `~/`），

```bash
$ git clone https://github.com/altercation/solarized.git
```
　　解压后找到iTerm2的目录，发现有两个配色文件。把它们从`Profiles`→`Colors`选项卡中`Load Presets`→`Import...`进来，选择其一即可。如果觉得颜色黯淡，可将`Profiles`→`Text`选项卡中勾掉`Draw bold text in bright colors`。

- 保留所有历史输出，`Profiles` → `Terminal`→`Scrollback Buffer`中勾选`Unlimited Scrollback`。


- 仍然使用上次会话的目录，在
  `Profiles` → `General`→`Working Directory` 中选择` Reuse previous session’s directory`。
- 静默提示音，在`Profiles` → `Terminal`→`Notifications`中勾选`Silence bell`。



### 配置zsh

macOS预装了6种shell版本，其中Z shell (zsh)被认为功能强大，可拓展性最强，但前期配置相当繁琐。所幸开源项目oh-my-zsh为zsh使用者提供了一键式配置方案。

macOS中自带的zsh版本较老，但不宜直接覆盖更新。可先通过Homebrew安装最新版zsh（若可以接受系统自带的zsh，可跳过相关步骤）。

```bash
$ brew install zsh

#版本号1：通过如下命令查看的“当前安装的zsh版本”
$ zsh --version

#版本号2：通过如下命令查看的“当前使用的zsh版本”（即系统预设的zsh版本）
$ echo $ZSH_VERSION
```

一般来说，版本号1比版本号2更新。下面修改默认Shell。

所有的系统Shell目录都保存在`/etc/shells`文件中。由于通过brew安装的zsh在`/usr/local`下，所以我们

```bash
$ sudo vi /etc/shells

#未经修改的shells文件有6行，分别对应macOS自带的6种shell
#在shells文件末尾加入一行
/usr/local/bin/zsh

#退出vim，输入如下命令，把系统使用的shell改为最新版的zsh
$ chsh -s /usr/local/bin/zsh
```

完成后重启iTerm2，此时使用的Shell就不再是bash了。再次检查当前使用的zsh版本，就和安装的版本相同了。

这样，若以后zsh再有更新，也只需用Homebrew更新即可：

```bash
$ brew reinstall zsh
```

然后就是重头戏，oh-my-zsh。有两种安装方式，推荐第二种：

```bash
$ curl -L https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh | sh
#或
$ wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | sh
```

完成后，打开`~/.zshrc`文件，内有全部的预设配置和说明，可以自行更改。下面仅列出几条：

```bash
#zsh主题，默认robbyrussell
ZSH_THEME="robbyrussell"

#用于隐藏路径前的那串用户名
DEFAULT_USER="userName"

#添加自己需要的插件
plugins=(git brew) 

#alias X="Y"，将Y简写为X，如
alias ..="cd .."
alias ga="git add"
```

更多zsh主题可在[这里](https://github.com/robbyrussell/oh-my-zsh/wiki/themes)预览。推荐avit，agnoster或ys。



更多的iTerm2、zsh的使用/配置技巧请参阅网络资料。



参考链接：

[【1】](http://yijiebuyi.com/blog/b9b5e1ebb719f22475c38c4819ab8151.html)	[【2】](http://yijiebuyi.com/blog/9c6419897949a7935d0fdec74cb7c61b.html)	[【3】](http://www.jianshu.com/p/bb1c97269b11)	[【4】](http://www.tuicool.com/articles/FFN7Vbq)	