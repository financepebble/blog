---
layout: page
title: "Financial News"
permalink: /market-news/
---

## Personal Finance News by Topic

<div style="margin-bottom: 20px;">
  <button onclick="loadNews('retirement')" style="padding: 10px 20px; margin: 5px; cursor: pointer; background: #2563eb; color: white; border: none; border-radius: 5px;">Retirement</button>
  <button onclick="loadNews('personal-finance')" style="padding: 10px 20px; margin: 5px; cursor: pointer; background: #2563eb; color: white; border: none; border-radius: 5px;">Personal Finance</button>
  <button onclick="loadNews('tax')" style="padding: 10px 20px; margin: 5px; cursor: pointer; background: #2563eb; color: white; border: none; border-radius: 5px;">Tax</button>
</div>

<div id="news-feed" style="margin-top: 30px;">
  <p>Click a topic above to load news...</p>
</div>

<script>
// RSS feeds focused on retirement, personal finance, and tax
const newsFeeds = {
  'retirement': [
    'https://www.marketwatch.com/rss/realtimeheadlines',
    'https://www.kiplinger.com/feeds/rss/retirement',
    'https://money.usnews.com/money/retirement/articles/feed'
  ],
  'personal-finance': [
    'https://www.nerdwallet.com/blog/feed/',
    'https://www.bankrate.com/f
