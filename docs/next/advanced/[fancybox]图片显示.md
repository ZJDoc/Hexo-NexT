
# [fancybox]图片显示

`hexo`页面大小有限，如果图片过大，会缩放在页面中

使用[fancybox](https://github.com/theme-next/theme-next-fancybox3)能够实现点击图片显示原先大小功能，还可以进一步放大

进入`NexT`主题路径，下载`fancybox`仓库

```
$ cd themes/next
$ git clone https://github.com/theme-next/theme-next-fancybox3 source/lib/fancybox
```

修改`NexT _config.yml`

```
# FancyBox is a tool that offers a nice and elegant way to add zooming functionality for images.
# For more information: https://fancyapps.com/fancybox
fancybox: false
```

设置属性`fancybox`为`true`，重新生成即可