---
layout: default
title: Blog
permalink: /blog/
---

<link rel="stylesheet" href="{{ '/assets/css/custom.css' | relative_url }}">

<div class="blog-header">
  <h1 style="font-family: 'Playfair Display', serif; font-size: 3rem; margin-bottom: 1rem; color: var(--text-primary);">All Blog Posts</h1>
  <p style="font-size: 1.2rem; color: var(--text-secondary); margin-bottom: 3rem;">Explore our complete collection of financial insights, tips, and strategies</p>
</div>

<div class="post-list-single-column">
  {% assign sorted_posts = site.posts | sort: 'date' | reverse %}
  {% for post in sorted_posts %}
    <div class="post-card-full-width">
      <div class="post-card-content">
        <div style="display: flex; gap: 1rem; align-items: center; margin-bottom: 0.5rem; flex-wrap: wrap;">
          <span class="post-meta">{{ post.date | date: "%b %-d, %Y" }}</span>
          {% if post.categories %}
            {% for category in post.categories limit:2 %}
              <span class="category-badge-small">{{ category }}</span>
            {% endfor %}
          {% endif %}
        </div>
        
        <h3 class="post-title-large">
          <a href="{{ post.url | relative_url }}">
            {{ post.title | escape }}
          </a>
        </h3>
        
        {% if post.excerpt %}
          <p class="post-excerpt-large">{{ post.excerpt | strip_html | truncatewords: 40 }}</p>
        {% endif %}
        
        {% if post.author %}
          <p class="post-author-small">By {{ post.author }}</p>
        {% endif %}
        
        <a href="{{ post.url | relative_url }}" class="read-more-link">Read more →</a>
      </div>
    </div>
  {% endfor %}
</div>

{% if site.posts.size == 0 %}
  <div class="info-box" style="margin-top: 3rem;">
    <p>No blog posts yet. Check back soon for financial insights and tips!</p>
  </div>
{% endif %}

<style>
/* Blog Page Specific Styles */
.blog-header {
  text-align: center;
  padding: 2rem 0 3rem;
  border-bottom: 2px solid var(--border-color);
  margin-bottom: 3rem;
}

.post-list-single-column {
  max-width: 900px;
  margin: 0 auto;
}

.post-card-full-width {
  background: var(--card-bg);
  border-radius: 16px;
  padding: 2rem;
  margin-bottom: 2rem;
  box-shadow: 0 2px 12px var(--shadow-color);
  transition: all 0.3s ease;
  border: 1px solid var(--border-color);
}

.post-card-full-width:hover {
  transform: translateY(-4px);
  box-shadow: 0 8px 24px var(--shadow-color);
  border-color: #1e40af;
}

.post-card-content {
  width: 100%;
}

.post-meta {
  color: var(--text-muted);
  font-size: 0.9rem;
  font-weight: 500;
}

.category-badge-small {
  display: inline-block;
  background: #eff6ff;
  color: #1e40af;
  padding: 0.25rem 0.75rem;
  border-radius: 12px;
  font-size: 0.75rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

[data-theme="dark"] .category-badge-small {
  background: rgba(30, 64, 175, 0.2);
  color: #60a5fa;
}

.post-title-large {
  font-family: 'Playfair Display', serif;
  font-size: 1.75rem;
  font-weight: 700;
  margin: 0.75rem 0;
  line-height: 1.3;
}

.post-title-large a {
  color: var(--text-primary);
  text-decoration: none;
  transition: color 0.3s;
}

.post-title-large a:hover {
  color: #1e40af;
}

.post-excerpt-large {
  color: var(--text-secondary);
  font-size: 1rem;
  line-height: 1.6;
  margin: 1rem 0;
}

.post-author-small {
  color: var(--text-muted);
  font-size: 0.85rem;
  font-style: italic;
  margin: 0.5rem 0;
}

.read-more-link {
  display: inline-flex;
  align-items: center;
  color: #1e40af;
  font-weight: 600;
  text-decoration: none;
  margin-top: 1rem;
  transition: all 0.3s;
}

.read-more-link:hover {
  color: #1e3a8a;
  transform: translateX(4px);
}

.info-box {
  background: #eff6ff;
  border: 2px solid #1e40af;
  border-radius: 12px;
  padding: 2rem;
  text-align: center;
}

[data-theme="dark"] .info-box {
  background: rgba(30, 64, 175, 0.1);
  border-color: #60a5fa;
}

/* Responsive */
@media (max-width: 768px) {
  .blog-header h1 {
    font-size: 2rem;
  }
  
  .blog-header p {
    font-size: 1rem;
  }
  
  .post-card-full-width {
    padding: 1.5rem;
  }
  
  .post-title-large {
    font-size: 1.4rem;
  }
  
  .post-excerpt-large {
    font-size: 0.95rem;
  }
}
</style>
