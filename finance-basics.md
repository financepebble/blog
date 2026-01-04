---
layout: page
title: Personal Finance
permalink: /finance-basics/
---

<link rel="stylesheet" href="{{ '/assets/css/custom.css' | relative_url }}">

# Personal Finance Basics

Welcome to your hub for mastering personal finance fundamentals. Whether you're just starting out or looking to optimize your money management, you'll find practical advice here.

## Popular Topics

<div class="portal-grid">
  <div class="portal-card">
    <div class="portal-icon">📋</div>
    <h3>Budgeting 101</h3>
    <p>Learn the 50/30/20 rule, zero-based budgeting, and other frameworks to take control of your spending.</p>
  </div>

  <div class="portal-card">
    <div class="portal-icon">🚨</div>
    <h3>Emergency Funds</h3>
    <p>How much to save, where to keep it, and when to use it. Build your financial safety net.</p>
  </div>

  <div class="portal-card">
    <div class="portal-icon">💸</div>
    <h3>Debt Management</h3>
    <p>Avalanche vs. snowball methods, debt consolidation, and strategies to become debt-free faster.</p>
  </div>

  <div class="portal-card">
    <div class="portal-icon">📈</div>
    <h3>Investing Basics</h3>
    <p>Index funds, ETFs, dollar-cost averaging, and how to start investing with confidence.</p>
  </div>

  <div class="portal-card">
    <div class="portal-icon">🏠</div>
    <h3>Rent vs. Buy</h3>
    <p>Use calculators and frameworks to decide whether renting or buying makes sense for you.</p>
  </div>

  <div class="portal-card">
    <div class="portal-icon">💼</div>
    <h3>Side Hustles</h3>
    <p>Generate extra income with proven side hustle ideas that fit your skills and schedule.</p>
  </div>
</div>

## Recent Personal Finance Posts

<ul class="post-list">
  {% for post in site.categories.finance limit:10 %}
    <li>
      <span class="post-meta">{{ post.date | date: "%b %-d, %Y" }}</span>
      <h3>
        <a class="post-link" href="{{ post.url | relative_url }}">
          {{ post.title | escape }}
        </a>
      </h3>
    </li>
  {% else %}
    <li>
      <p style="color: #64748b;">Posts coming soon! Check back regularly for new content.</p>
    </li>
  {% endfor %}
</ul>

---

<div class="info-box">
  <strong>💡 Pro Tip:</strong> Start with budgeting and emergency funds before diving into investing. A solid foundation makes everything else easier.
</div>
