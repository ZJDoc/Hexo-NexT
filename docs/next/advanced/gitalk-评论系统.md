
# [Gitalk]评论系统

`NexT`集成了多种评论系统，当前使用`Gitalk`

## 简介

[gitalk](https://github.com/gitalk/gitalk/blob/master/readme-cn.md)是一个基于`github`开发的评论插件，它将文章评论以`issues`形式保存在`github`仓库中

实现步骤如下：

1. 注册`github`应用
2. `NexT`配置

## 注册github应用

进入`github`注册页面：[Register a new OAuth application ](https://github.com/settings/applications/new)

![](./imgs/register-github.png)

* `Application name`：应用名，方便起见直接填`github`用户名
* `Homepage URL`：网站地址
* `Application description`：应用描述
* `Authorization callback URL`：网站地址

注册成功后会生成`Client ID`和`Client Secret`

## NexT配置

修改主题`_config.yml`

```
# Gitalk
# Demo: https://gitalk.github.io
# For more information: https://github.com/gitalk/gitalk
gitalk:
  enable: false
  github_id: # GitHub repo owner
  repo: # Repository name to store issues
  client_id: # GitHub Application Client ID
  client_secret: # GitHub Application Client Secret
  admin_user: # GitHub repo owner and collaborators, only these guys can initialize gitHub issues
  distraction_free_mode: true # Facebook-like distraction free mode
  # Gitalk's display language depends on user's browser or system environment
  # If you want everyone visiting your site to see a uniform language, you can set a force language value
  # Available values: en | es-ES | fr | ru | zh-CN | zh-TW
  language:
```

* 设置`enable`为`true`
* `github_id`填入`github`帐号
* `repo`填入`github`仓库名（**注意：是仓库名不是仓库地址**），评论将会以`issues`形式保存在该仓库下
* `client_id`填入注册生成的值
* `client_secret`填入注册生成的值
* `admin_user`填入`github`帐号，用于初始化评论账户

## `Error: Not Found`

问题描述：在文章底部评论框中出现错误信息

    Error: Not Found

解决：和配置选项的填写有关，注意填写的内容

## 隐藏评论框

设置`gitalk`评论系统后，将会在每篇文章末尾添加评论框，而对于标签页/类别页等不需要评论的文章，可在`front-matter`设置属性进行隐藏

    comments: false

## 相关阅读

* [Gitalk](https://theme-next.js.org/docs/third-party-services/comments.html)
* [Hexo 搭建：配置 Gitalk 评论系统](https://blog.csdn.net/qq_36537546/article/details/90730412)
* [gitalk提示Error Not Found #130](https://github.com/Molunerfinn/hexo-theme-melody/issues/130)
* [gitalk/gitalk](https://github.com/gitalk/gitalk/blob/master/readme-cn.md)
* [Hexo中Gitalk配置使用教程-可能是目前最详细的教程 | ioChen's Blog #3](https://github.com/iosite/gitalk/issues/3)
* [ hexo next 主题配置 gitalk 评论后无法初始化创建 issue #115 ](https://github.com/gitalk/gitalk/issues/115)