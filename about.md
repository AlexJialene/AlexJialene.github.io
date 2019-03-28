---
layout: page
title: 关于
permalink: about.html
image: /public/images/redflag.jpg
order: 5
---

{% if site.author.photo %}
![{{ site.author.name }}]({{ site.author.photo | prepend: site.cdnurl }}){:.me}
{% endif %}

90后的一个懒癌骚年，纯种软工Java。博客比较少更新；只有在想起来 && 有时间的时候可能会写一篇。然后好像也没什么其他说的。

## 联系
* alexdennis.lam@qq.com
* alexdennis.lam@gmail.com
* [Github](https://github.com/AlexJialene){:target="_blank"}




## 版权说明

我坚信着开放、自由和乐于分享是推动计算机技术发展的动力之一。所以本站所有内容均采用[署名 4.0 国际（CC BY
4.0）](http://creativecommons.org/licenses/by/4.0/deed.zh)创作共享协议。通俗地讲，只要在使用时署名，那么使用者可以对本站所有内容进行转载、节选、二次创作，并且允许商业性使用。

## 其他

我的博客使用 Jekyll 搭建，感谢 [biezhi](https://github.com/biezhi/blog){:target="_blank"} 的技术支持。
另外若发现本站有任何侵犯您利益的内容，请及时邮件或留言联系，我会第一时间删除所有相关内容。

<!-- Add Disqus Comments -->
{% if site.disqus %}
{% include disqus.html %}
{% endif %}