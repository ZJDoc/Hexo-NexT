
# RSS支持

## 下载

```
$ npm install hexo-generator-feed --save
```

## Hexo _config.yml

在底部添加如下设置

```
feed:
  enable: true
  type: atom
  path: atom.xml
  limit: 20
  hub:
  content:
  content_limit: 140
  content_limit_delim: ' '
  order_by: -date
  icon: icon.png
  autodiscovery: true
  template:
```

* `type`：制定类型
* `path`：生成路径
* `limit`：文章数量。使用`0`或`false`表示所有文章
* `content_limit`：文章内容限制
* `order_by`：排序

## NexT _config.yml

`NexT`提供了两个地方进行`RSS`展示

1. 在菜单栏显示

        # Usage: `Key: /link/ || icon`
        # Key is the name of menu item. If the translation for this item is available, the translated text will be loaded, otherwise the Key name will be used. Key is case-senstive.
        # Value before `||` delimiter is the target link, value after `||` delimiter is the name of Font Awesome icon.
        # External url should start with http:// or https://
        menu:
          home: / || fa fa-home
          about: /about/ || fa fa-user
          tags: /tags/ || fa fa-tags
          categories: /categories/ || fa fa-th
          archives: /archives/ || fa fa-archive
          RSS: /atom.xml || fa fa-rss
        
2. 在文章底部显示

        # Subscribe through Telegram Channel, Twitter, etc.
        # Usage: `Key: permalink || icon` (Font Awesome)
        follow_me:
          #Twitter: https://twitter.com/username || fab fa-twitter
          #Telegram: https://t.me/channel_name || fab fa-telegram
          #WeChat: /images/wechat_channel.jpg || fab fa-weixin
          # RSS: /atom.xml || fa fa-rss

## 相关阅读

* [hexojs/hexo-generator-feed](https://github.com/hexojs/hexo-generator-feed)
* [Follow Me](https://theme-next.js.org/docs/theme-settings/posts.html?highlight=rss)