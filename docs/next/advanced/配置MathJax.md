# 配置MathJax

参考：

[数学公式](https://github.com/theme-next/hexo-theme-next/blob/master/docs/zh-CN/MATH.md)

[Math Equations](https://theme-next.org/docs/third-party-services/math-equations)

配置`NexT`主题支持数学公式，分为两步

1. 打开`NexT`内部数学公式渲染引擎
2. 打开`hexo`渲染器

## 打开NexT内部数学公式渲染引擎

进入`themes/next/_config.yml`，找到`math`配置

```
# Math Formulas Render Support
math:
  # Default (true) will load mathjax / katex script on demand.
  # That is it only render those page which has `mathjax: true` in Front-matter.
  # If you set it to false, it will load mathjax / katex srcipt EVERY PAGE.
  per_page: true

  # hexo-renderer-pandoc (or hexo-renderer-kramed) required for full MathJax support.
  mathjax:
    enable: true
    # See: https://mhchem.github.io/MathJax-mhchem/
    mhchem: false

  # hexo-renderer-markdown-it-plus (or hexo-renderer-markdown-it with markdown-it-katex plugin) required for full Katex support.
  katex:
    enable: false
    # See: https://github.com/KaTeX/KaTeX/tree/master/contrib/copy-tex
    copy_tex: false
```

属性`per_page`表示是否自动渲染每一页，如果为`true`就只渲染配置块中包含`mathjax: true`的文章

    ---
    title: Next Post
    date: 2019-01-19 17:36:13
    mathjax: true
    ---

设置`mathjax`属性`enable`为`true`

## 打开`hexo`渲染器

参考：[sun11/hexo-renderer-kramed](https://github.com/sun11/hexo-renderer-kramed)

进入网站根目录

    $ npm uninstall hexo-renderer-marked --save
    $ npm install hexo-renderer-kramed --save

数学公式如下

    Simple inline $a = b + c$.

    $$
    \frac{\partial u}{\partial t}
    = h^2 \left( \frac{\partial^2 u}{\partial x^2} +
    \frac{\partial^2 u}{\partial y^2} +
    \frac{\partial^2 u}{\partial z^2}\right)
    $$

启动服务器

    $ hexo clean && hexo generate && hexo server

![](./imgs/hexo-math.png)

## 行内公式渲染不完全

当前我遇到的情况是一行只能渲染一个行内公式，多个公式一起就不成功了

参考[hexo Next主题中支持latex公式(转) ](http://layty.coding.me/2018/09/21/hexo/hexo-Next%E4%B8%BB%E9%A2%98%E4%B8%AD%E6%94%AF%E6%8C%81latex%E5%85%AC%E5%BC%8F/)，渲染插件`hexo-renderer-kramed`针对行内公式渲染有语义冲突，比如对于下划线等符号会转换成`markdown`语法

进入`node_modules/kramed/lib/rules/inline.js`

修改`11`行`escape`变量

```
// escape: /^\\([\\`*{}\[\]()#$+\-.!_>])/,
escape: /^\\([`*\[\]()#$+\-.!_>])/,
```

修改`20`行`em`变量

```
// em: /^\b_((?:__|[\s\S])+?)_\b|^\*((?:\*\*|[\s\S])+?)\*(?!\*)/,
em: /^\*((?:\*\*|[\s\S])+?)\*(?!\*)/,
```

重新生成即可

**注意：如果使用`CI`进行编译生成，需要在编译之前进行修改，比如文件替换**