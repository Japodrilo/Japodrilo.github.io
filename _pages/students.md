---
layout: default
title: supervision
permalink: /students/
nav: true
nav_order: 3
---

<div class="post">

  <header class="post-header">
    <h1 class="post-title">{{ page.title }}</h1>
    <p class="post-description">supervised students & postdocs</p>
  </header>

  <article>
    {% assign level_order = "postdoc,phd,masters,undergraduate" | split: "," %}

    {% for level in level_order %}
      {% assign level_students = site.data.students | where: "level", level %}

      {% if level_students.size > 0 %}
        <h2 class="category" style="margin-top: 3rem; border-bottom: 1px solid var(--global-divider-color); padding-bottom: 5px;">
          {% if level == "postdoc" %}postdoctoral researchers{% else %}{{ level | replace: "phd", "ph.d." }} students{% endif %}
        </h2>

        {% assign sorted_students = level_students | sort: "year_start" | reverse %}

        <ul class="post-list" style="list-style: none; padding-left: 0;">
        {% for student in sorted_students %}

          {% comment %} Reduced margin from 2.5rem to 1.5rem to tighten the list {% endcomment %}
          <li style="margin-bottom: -1.5rem;">
            <div class="row">
              <div class="col-sm-12">

                {% comment %} Name with optional external link {% endcomment %}
                <h3 class="post-title" style="font-size: 1.3rem; margin-bottom: 0.4rem;">
                  {% if student.url %}
                    <a href="{{ student.url }}" target="_blank">{{ student.name }} <i class="fa-solid fa-arrow-up-right-from-square fa-xs"></i></a>
                  {% else %}
                    {{ student.name }}
                  {% endif %}
                </h3>

                {% comment %} Metadata with Colored Date Badge {% endcomment %}
                <p class="post-meta" style="margin-bottom: 0.8rem; font-size: 0.95rem; color: var(--global-text-color-light); display: flex; align-items: center; flex-wrap: wrap; gap: 10px;">

                  {% comment %} The Date Box {% endcomment %}
                  <span class="badge" style="background-color: var(--global-theme-color); color: var(--global-bg-color); font-size: 0.85rem; padding: 0.4em 0.6em; font-weight: 600;">
                    {{ student.year_start }} – {{ student.year_end }}
                  </span>

                  {% comment %} Program and Institution {% endcomment %}
                  <span>
                    {{ student.program }} &nbsp;&middot;&nbsp; <span style="font-style: italic;">{{ student.institution }}</span>
                  </span>
                </p>

                {% comment %} Research Topic {% endcomment %}
                <div class="post-description" style="margin-top: -0.6rem; margin-bottom:-0.8rem; line-height: 1.5;">
                  <strong style="color: var(--global-theme-color);">Project:</strong> {{ student.topic }}
                </div>

              </div>
            </div>
          </li>
        {% endfor %}
        </ul>
      {% endif %}
    {% endfor %}

  </article>

</div>
