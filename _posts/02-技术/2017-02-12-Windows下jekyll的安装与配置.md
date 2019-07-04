---
layout: post
title: Windows下jekyll的安装与配置
category: 技术
---

## 安装RubyInstallers for Windows

切换源(注意用的是http不是https)
```
gem sources --remove https://rubygems.org/  
gem sources -a http://gems.ruby-china.org/
gem souces -l
# 确保只有 gems.ruby-china.org

$gem update --system # 这里可能需要翻墙一下
$gem -v
2.6.7
```

![图片](http://i2.muimg.com/589926/5905eaa42d2d6c0d.png)


## 安装jekyll

```
gem install jekyll bundler
jekyll new site
cd site
jekyll serve
```

打开浏览器 `http://localhost:4000`


## GitHub 仓库

![GitHub 仓库设置](http://pic.yupoo.com/bztd/gVC4rFI6/39e9ec31.png)

相关链接：
[RubyInstallers](http://rubyinstaller.org/downloads/)
[jekyll中文](http://jekyll.com.cn/)
[GitHub Pages](https://pages.github.com)