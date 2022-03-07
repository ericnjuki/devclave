---
layout: default
title: Blog
permalink: /blog/
---

<div class="container">
  <div class="row">
    <div class="col-md-8 col-md-push-2 wrapper">
      <main aria-label="Content">
        <div class="row">
          <div class="main-content">
            <div class="home-links">
                {%- if site.posts.size > 0 -%}
                <!-- <h2>{{ page.list_title | default: "Posts" }}</h2> -->
                <ul class="topics aspnet">
                  <li class="topic-header">
                    <h2>Posts</h2>
                  </li>
                  {%- for post in site.posts -%}
                  <li class="article-title">
                    {%- assign date_format = site.minima.date_format | default: "%b %-d, %Y" -%}
                    <!-- <h3> -->
                      <a href="{{ post.url | relative_url }}">
                        {{ post.title | escape }}
                      </a>
                      <span class="post-date">{{ post.date | date: date_format }}</span>
                    <!-- </h3> -->
                    <!-- {%- if site.show_excerpts -%}
                      {{ post.excerpt }}
                    {%- endif -%} -->
                  </li>
                  {%- endfor -%}
                </ul>
              {%- endif -%}
            </div>
          </div>
        </div>
      </main>
    </div>
  </div>
  {%- include footer.html -%}
</div>