---
title: 4. 使用jekyl添加latex支持
date: 2022-12-30
tags: jekyll
---

## 步骤
- 将下面代码添加到default的layout中
```js
<script type="text/x-mathjax-config">
    MathJax.Hub.Config({
      tex2jax: {
        skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'],
        inlineMath: [['$','$']]
      }
    });
</script>
<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>
```

## 参考
- [jekyll下Markdown的填坑技巧](https://eipi10.cn/others/2019/12/07/jekyll-markdown-skills/)