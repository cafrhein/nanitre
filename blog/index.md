---
layout: default
title: Blog
---

<header style="margin-bottom: 4rem;">
    <h1 style="font-size: 2.5rem; font-weight: 300; letter-spacing: -1px;">Blog</h1>
    <p style="color: var(--secondary-color);">Procesos creativos, noticias y reflexiones sobre arte y UX.</p>
</header>

<section class="blog-list">
    {% for post in site.posts %}
    <article style="margin-bottom: 4rem; display: grid; grid-template-columns: 200px 1fr; gap: 2rem; align-items: baseline;">
        <time style="font-size: 0.8rem; color: var(--secondary-color); text-transform: uppercase;">
            {{ post.date | date: "%d · %m · %Y" }}
        </time>
        <div>
            <h2 style="margin: 0 0 0.5rem 0; font-size: 1.5rem; font-weight: 600;">
                <a href="{{ post.url | relative_url }}" style="text-decoration: none; color: inherit; transition: opacity 0.3s;" onmouseover="this.style.opacity='0.6'" onmouseout="this.style.opacity='1'">
                    {{ post.title }}
                </a>
            </h2>
            <p style="margin: 0; color: var(--secondary-color); font-size: 1rem;">
                {{ post.excerpt | strip_html | truncatewords: 30 }}
            </p>
        </div>
    </article>
    {% endfor %}
</section>
