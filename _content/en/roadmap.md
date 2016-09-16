---
permalink: /roadmap/
layout: index_tech
title: Roadmap
redirect_from:

---

# Roadmap

 Steem.it and Steem have a long roadmap for future enhancements to the website and protocol. This page
 will be updated with information about future features and changes.

-----

{% assign documentation = (site.roadmap | where: 'lang', page.lang | sort: 'priority') %}
{% for doc in documentation  %}
<div class="row tech-toc">


  <div class="col-md-2 center tech-toc-img">
    <img class="tech-toc hidden-xs" src="{{ BASE_PATH }}/{{ doc.image }}" />
  </div>
  <div class="col-md-10 ">
   <h3 class="tech-title"><a href="{{ doc.url }}">{{ doc.title }}</a> - {{ doc.subtitle }}</h3>

    {{ doc.summary }}
  </div>

</div>
{% endfor %}
