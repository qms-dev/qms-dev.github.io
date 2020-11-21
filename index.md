---
layout: default
title: Home
nav_order: 1
description: "qms-dev团队开发文档"
permalink: /
---

# qms-dev团队开发文档
{: .fs-9 }

这是qms-dev团队的所有开发文档，托管在Github
{: .fs-6 .fw-300 }

[Get started now](#getting-started){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 } [View it on GitHub](https://github.com/pmarsceill/just-the-docs){: .btn .fs-5 .mb-4 .mb-md-0 }

---

#### 感谢以下人员对此开发者文档的贡献!

<ul class="list-style-none">
{% for contributor in site.github.contributors %}
  <li class="d-inline-block mr-1">
     <a href="{{ contributor.html_url }}"><img src="{{ contributor.avatar_url }}" width="32" height="32" alt="{{ contributor.login }}"/></a>
  </li>
{% endfor %}
</ul>
