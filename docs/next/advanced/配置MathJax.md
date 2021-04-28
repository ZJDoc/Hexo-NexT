# 配置MathJax

`NexT`默认使用`hexo-renderer-marked`进行公式渲染，同时额外提供了两种方式来优化公式渲染

* `hexo-renderer-pandoc`：基于`MathJax`
* `hexo-renderer-markdown-it-plus/hexo-renderer-markdown-it`：基于`KeTex`

经过测试发现，`hexo-renderer-pandoc`提供了最大程度的兼容语法以及渲染性能

## NexT _config.yml

```
# Math Formulas Render Support
# Warning: Please install / uninstall the relevant renderer according to the documentation.
# See: https://theme-next.js.org/docs/third-party-services/math-equations
# Server-side plugin: https://github.com/next-theme/hexo-filter-mathjax
math:
  # Default (false) will load mathjax / katex script on demand.
  # That is it only render those page which has `mathjax: true` in front-matter.
  # If you set it to true, it will load mathjax / katex srcipt EVERY PAGE.
  every_page: true            ---------------------> 设置为true

  mathjax:
    enable: true                   ---------------------> 设置为true
    # Available values: none | ams | all
    tags: none

  katex:
    enable: false
    # See: https://github.com/KaTeX/KaTeX/tree/master/contrib/copy-tex
    copy_tex: false
```

* 属性`every_page`表示是否自动渲染每一页
* 如果为`false`就只渲染配置块中包含`mathjax: true`的文章

```
    ---
    title: Next Post
    ...
    ...
    mathjax: true
    ---
```

## 安装

* 安装插件

```
$ npm un hexo-renderer-marked
$ npm i hexo-renderer-pandoc
```

* 额外需要安装[pandoc](https://github.com/jgm/pandoc/blob/master/INSTALL.md)

## [ERROR][hexo-renderer-pandoc] pandoc exited with code 9

* 问题描述

```
INFO  Start processing
ERROR {
  err: Error: 
  [ERROR][hexo-renderer-pandoc] On /var/jenkins_home/workspace/hexo-blog-docker/docs/themes/next/languages/README.md
  [ERROR][hexo-renderer-pandoc] pandoc exited with code 9: pandoc: Unknown extension: smart
  
      at Hexo.pandocRenderer (/var/jenkins_home/workspace/hexo-blog-docker/docs/node_modules/hexo-renderer-pandoc/index.js:114:11)
      at Hexo.tryCatcher (/var/jenkins_home/workspace/hexo-blog-docker/docs/node_modules/bluebird/js/release/util.js:16:23)
      at Hexo.<anonymous> (/var/jenkins_home/workspace/hexo-blog-docker/docs/node_modules/bluebird/js/release/method.js:15:34)
      at /var/jenkins_home/workspace/hexo-blog-docker/docs/node_modules/hexo/lib/hexo/render.js:75:22
      at tryCatcher (/var/jenkins_home/workspace/hexo-blog-docker/docs/node_modules/bluebird/js/release/util.js:16:23)
      at Promise._settlePromiseFromHandler (/var/jenkins_home/workspace/hexo-blog-docker/docs/node_modules/bluebird/js/release/promise.js:547:31)
      at Promise._settlePromise (/var/jenkins_home/workspace/hexo-blog-docker/docs/node_modules/bluebird/js/release/promise.js:604:18)
      at Promise._settlePromise0 (/var/jenkins_home/workspace/hexo-blog-docker/docs/node_modules/bluebird/js/release/promise.js:649:10)
      at Promise._settlePromises (/var/jenkins_home/workspace/hexo-blog-docker/docs/node_modules/bluebird/js/release/promise.js:729:18)
      at _drainQueueStep (/var/jenkins_home/workspace/hexo-blog-docker/docs/node_modules/bluebird/js/release/async.js:93:12)
      at _drainQueue (/var/jenkins_home/workspace/hexo-blog-docker/docs/node_modules/bluebird/js/release/async.js:86:9)
      at Async._drainQueues (/var/jenkins_home/workspace/hexo-blog-docker/docs/node_modules/bluebird/js/release/async.js:102:5)
      at Immediate.Async.drainQueues [as _onImmediate] (/var/jenkins_home/workspace/hexo-blog-docker/docs/node_modules/bluebird/js/release/async.js:15:14)
      at processImmediate (internal/timers.js:461:21)
} Process failed: %s languages/README.md
FATAL {
  err: Error: 
  [ERROR][hexo-renderer-pandoc] On /var/jenkins_home/workspace/hexo-blog-docker/docs/source/_posts/dataset/制作图像数据集.md
  [ERROR][hexo-renderer-pandoc] pandoc exited with code 9: pandoc: Unknown extension: smart
  
      at Hexo.pandocRenderer (/var/jenkins_home/workspace/hexo-blog-docker/docs/node_modules/hexo-renderer-pandoc/index.js:114:11)
      at Hexo.tryCatcher (/var/jenkins_home/workspace/hexo-blog-docker/docs/node_modules/bluebird/js/release/util.js:16:23)
      at Hexo.<anonymous> (/var/jenkins_home/workspace/hexo-blog-docker/docs/node_modules/bluebird/js/release/method.js:15:34)
      at /var/jenkins_home/workspace/hexo-blog-docker/docs/node_modules/hexo/lib/hexo/render.js:75:22
      at tryCatcher (/var/jenkins_home/workspace/hexo-blog-docker/docs/node_modules/bluebird/js/release/util.js:16:23)
      at Promise._settlePromiseFromHandler (/var/jenkins_home/workspace/hexo-blog-docker/docs/node_modules/bluebird/js/release/promise.js:547:31)
      at Promise._settlePromise (/var/jenkins_home/workspace/hexo-blog-docker/docs/node_modules/bluebird/js/release/promise.js:604:18)
      at Promise._settlePromiseCtx (/var/jenkins_home/workspace/hexo-blog-docker/docs/node_modules/bluebird/js/release/promise.js:641:10)
      at _drainQueueStep (/var/jenkins_home/workspace/hexo-blog-docker/docs/node_modules/bluebird/js/release/async.js:97:12)
      at _drainQueue (/var/jenkins_home/workspace/hexo-blog-docker/docs/node_modules/bluebird/js/release/async.js:86:9)
      at Async._drainQueues (/var/jenkins_home/workspace/hexo-blog-docker/docs/node_modules/bluebird/js/release/async.js:102:5)
      at Immediate.Async.drainQueues [as _onImmediate] (/var/jenkins_home/workspace/hexo-blog-docker/docs/node_modules/bluebird/js/release/async.js:15:14)
      at processImmediate (internal/timers.js:461:21)
} Something's wrong. Maybe you can find the solution here: %s https://hexo.io/docs/troubleshooting.html
```

* 解决方案：安装最新的[pandoc](https://github.com/jgm/pandoc/blob/master/INSTALL.md)

## 相关阅读

* [Math Equations](https://theme-next.js.org/docs/third-party-services/math-equations.html?highlight=mathjax)
* [数学公式](https://github.com/theme-next/hexo-theme-next/blob/master/docs/zh-CN/MATH.md)