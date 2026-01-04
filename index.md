---
layout: default
title: Home
---

<link rel="stylesheet" href="{{ '/assets/css/custom.css' | relative_url }}">

<div class="hero-section">
  <h1>Welcome to FinancePebble</h1>
  <p>Your comprehensive portal for smart financial decisions. Explore retirement planning, tax strategies, credit card optimization, exclusive deals, and classic travel destinations—all designed for people serious about their money.</p>
</div>

<div class="portal-grid">
  <a href="{{ '/finance-basics/' | relative_url }}" class="portal-card">
    <div class="portal-icon">💰</div>
    <div class="portal-card-content">
      <h3>Personal Finance</h3>
      <p>Master budgeting, saving strategies, emergency funds, and debt management. Build a solid financial foundation.</p>
    </div>
  </a>

  <a href="{{ '/retirement/' | relative_url }}" class="portal-card">
    <div class="portal-icon">🏖️</div>
    <div class="portal-card-content">
      <h3>Early Retirement</h3>
      <p>Learn FIRE principles, 401(k) strategies, and IRA options. Discover how to retire years—or decades—earlier.</p>
    </div>
  </a>

  <a href="{{ '/tax-tips/' | relative_url }}" class="portal-card">
    <div class="portal-icon">📊</div>
    <div class="portal-card-content">
      <h3>Tax Strategies</h3>
      <p>Maximize deductions, understand tax-loss harvesting, leverage HSAs, and plan for year-end tax optimization.</p>
    </div>
  </a>

  <a href="{{ '/credit-cards/' | relative_url }}" class="portal-card">
    <div class="portal-icon">💳</div>
    <div class="portal-card-content">
      <h3>Credit Card Rewards</h3>
      <p>Find the best sign-up bonuses, rewards programs, and cashback opportunities. Make your spending work for you.</p>
    </div>
  </a>

  <a href="{{ '/deals/' | relative_url }}" class="portal-card">
    <div class="portal-icon">🎯</div>
    <div class="portal-card-content">
      <h3>Fantastic Deals</h3>
      <p>Curated daily deals and discounts. Never miss an opportunity to save on products and services you need.</p>
    </div>
  </a>

  <a href="{{ '/travel/' | relative_url }}" class="portal-card">
    <div class="portal-icon">✈️</div>
    <div class="portal-card-content">
      <h3>Classic Travel</h3>
      <p>Explore timeless destinations on a budget. Learn to maximize points, miles, and travel insurance benefits.</p>
    </div>
  </a>

  <a href="{{ '/market-news/' | relative_url }}" class="portal-card">
    <div class="portal-icon">📰</div>
    <div class="portal-card-content">
      <h3>Financial News</h3>
      <p>Stay updated with retirement, personal finance, and tax news. Includes live market data and calculators.</p>
    </div>
  </a>
</div>

<div class="info-box">
  <h3 style="margin-top: 0; color: #1e40af;">📘 New to FinancePebble?</h3>
  <p>Start with our <a href="{{ '/finance-basics/' | relative_url }}" style="color: #1e40af; font-weight: 600;">Personal Finance basics</a> or jump directly to topics that interest you. We publish daily insights to help you make smarter money decisions.</p>
</div>

<div class="section-header">
  <h2 class="section-title">Latest Posts</h2>
</div>

<ul class="post-list">
  {% for post in site.posts limit:6 %}
    <li>
      <div class="post-list-content">
        <span class="post-meta">{{ post.date | date: "%b %-d, %Y" }}</span>
        <a class="post-link" href="{{ post.url | relative_url }}">
          {{ post.title | escape }}
        </a>
        {% if post.excerpt %}
          <p class="post-excerpt">{{ post.excerpt | strip_html | truncatewords: 30 }}</p>
        {% endif %}
      </div>
    </li>
  {% endfor %}
</ul>

<div style="text-align: center; margin-top: 3rem;">
  <a href="{{ '/blog/' | relative_url }}" class="btn">View All Posts</a>
</div>
