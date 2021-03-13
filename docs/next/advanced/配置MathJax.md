# 配置MathJax

`NexT`内置了数学公式渲染

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
  every_page: true

  mathjax:
    enable: true
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

## 相关阅读

* [Math Equations](https://theme-next.js.org/docs/third-party-services/math-equations.html?highlight=mathjax)
* [数学公式](https://github.com/theme-next/hexo-theme-next/blob/master/docs/zh-CN/MATH.md)