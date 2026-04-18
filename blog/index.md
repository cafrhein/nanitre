---
layout: default
title: Blog
---

<header style="margin-bottom: 4rem;">
    <h1 style="font-size: 2.5rem; font-weight: 300; letter-spacing: -1px;">Blog</h1>
    <p style="color: var(--secondary-color);">Procesos creativos, noticias y reflexiones sobre arte.</p>
</header>

<section class="grid-layout">
    {% for post in site.posts %}
    <article style="border-bottom: 1px solid #f0f0f0; padding-bottom: 2rem; margin-bottom: 2rem;">
        <time style="font-size: 0.75rem; color: var(--secondary-color); text-transform: uppercase; letter-spacing: 0.05em; display: block; margin-bottom: 0.5rem;">
            {{ post.date | date: "%d · %m · %Y" }}
        </time>
        <h2 style="margin: 0 0 1rem 0; font-size: 1.5rem; font-weight: 600; line-height: 1.2;">
            <a href="{{ post.url | relative_url }}" style="text-decoration: none; color: inherit; transition: var(--transition);" onmouseover="this.style.opacity='0.6'" onmouseout="this.style.opacity='1'">
                {{ post.title }}
            </a>
        </h2>
        <p style="margin: 0; color: var(--secondary-color); font-size: 0.95rem; line-height: 1.6;">
            {{ post.excerpt | strip_html | truncatewords: 25 }}
        </p>
        <a href="{{ post.url | relative_url }}" style="display: inline-block; margin-top: 1.5rem; font-size: 0.8rem; text-transform: uppercase; font-weight: 600; color: var(--primary-color); text-decoration: none; border-bottom: 1px solid var(--primary-color);">
            Leer más
        </a>
    </article>
    {% endfor %}
</section>
