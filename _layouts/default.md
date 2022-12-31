---
date created: 星期五, 十二月 30日 2022, 7:17:09 晚上
date modified: 星期六, 十二月 31日 2022, 5:30:55 下午
---
<!DOCTYPE html>

<script type="text/x-mathjax-config">
    MathJax.Hub.Config({
      tex2jax: {
        skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'],
        inlineMath: [['$','$']]
      }
    });
</script>
<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

<html lang="en">
  {% include head.html %}
  <body>
    <nav>{% include nav.html %}</nav>
    <div class="wrapper">
      <main>{{ content }}</main>
      <footer>{% include footer.html %}</footer>
    </div>

    {% include link-previews.html wrapperQuerySelector="content" %}
  </body>
</html>
