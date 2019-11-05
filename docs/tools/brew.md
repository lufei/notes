Homebrew 简称 brew，Homebrew 是一款 Mac OS 平台下的软件包管理工具，很方便帮助我们实现安装、卸载、更新、查看、搜索等很多实用的功能。

## 安装

```shell
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

## 配置镜像
```shell
cd "$(brew --repo)"
git remote set-url origin https://mirrors.ustc.edu.cn/brew.git
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
git remote set-url origin https://mirrors.ustc.edu.cn/homebrew-core.git
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-cask"
git remote set-url origin https://mirrors.ustc.edu.cn/homebrew-cask.git
brew update
echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.ustc.edu.cn/homebrew-bottles' >> ~/.bash_profile
```

## 常用命令

```shell
#查询 Homebrew 版本
brew -v

#brew帮助
brew -h

#更新Homebrew
brew update

#安装
brew install <pkg_name>

#卸载
brew uninstall <pkg_name>

#搜索
brew search <pkg_name>

#列出安装列表
brew list

#查看包内容信息
brew info <pkg_name>

#更新包
brew upgrade <pkg_name>

#删除具体旧软件
brew cleanup <pkg_name>

#删除所有旧软件
brew cleanup

#列出所有安装的软件里可以升级的
brew outdated		
```

## brew 和 brew cask 的区别

* brew 主要用来下载一些不带界面的命令行下的工具和第三方库来进行二次开发
* brew cask 主要用来下载一些带界面的应用软件，下载好后会自动安装，并能在 Mac 中直接运行使用