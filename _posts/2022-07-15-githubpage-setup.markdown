---
title:  "Github Page Set-up"
date:   2022-07-15 11:40:30 +0800
categories:
  - Website
tag:
  - set-up
toc: true
toc_sticky: true
---

## 写一个page
文件名：`yyyy-mm-dd-lowercase-name.markdown`   
YAML头：  
```yaml
---
title:  "Title"
date: 2023-07-15 11:40:30 +0800
last_modified_at: 2023-01-08 20:32:00 +0800
categories:
 - website
tag:
 - GithubPage
toc: true
toc_sticky: true
---
```
> layout: `post`  
> categories: `Network`, `Website`, `Linux`, `Log`, `Formal Method`  
> tag: `set-up`, `coq`, `sat`    

## github page 加密
1. 写出一个Markdown文件，导出为html文件  
> [HedgeDoc](https://demo.hedgedoc.org/)  
2. 使用[staticrypt](https://github.com/robinmoisson/staticrypt)项目：`staticrypt test.html MY_PASSPHRASE`  
> npm 查看：`npm -v`  
3. 加密后的html文件内容粘贴到 github page 的 YAML 标头后  


## 安装过程中的problems

> 主要参考了[Github Docs: Github Pages][github-doc-page]  
> 设备和使用的工具如下

| 设备&软件 | 版本 |
| ---- | ---- |
| MacBookPro | Monterery 12.4 |
| home brew | 3.5.4 |

主要流程就是参考docs，先用homebrew下载了chruby和ruby-install，然后用ruby- install下载了ruby，然后用gem安装了bundler和jekyll。
过程中遇到了几个问题，记录下来。

### ruby-install failed to download ruby
{% highlight shell %}
ruby-install ruby
{% endhighlight %}
在用chruby，ruby-install时，在第一行下载ruby版本时就出现下载错误。遍寻无果后，用ping和curl测试，ping可以，curl不行。然后再查找问题原因，参考stackoverflow [curl:Connection refused][stack-1]，解决了，确认是DNS的问题（8.8.8.8是谷歌DNS，国内的DNS需另外查询）。

### bundle exec jekyll serve: cannot load such file
用`bundle exec jekyll serve`在本地试运行时，出现了不能加载文件错误，参考github jekyll这个issue [Jekyll serve fails on Ruby 3.0][github-1]，解决了。

## others
### homebrew一键安装
这里再记录一个找到的homebrew一键安装，中科大镜像。  
`/bin/bash -c "$(curl -fsSL https://gitee.com/ineo6/homebrew-install/raw/master/install.sh)"`  
来源于这个网站：[Homebrew macOS 飞速安装教程][homebrew-setup]

[stack-1]: https://stackoverflow.com/questions/59572626/curl-7-failed-to-connect-to-raw-githubusercontent-com-port-443-connection-re
[github-doc-page]: https://docs.github.com/cn/pages
[github-1]: https://github.com/jekyll/jekyll/issues/8523
[homebrew-setup]: https://brew.idayer.com/
