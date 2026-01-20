---
layout: page
title: Financial News
permalink: /market-news/
---

<link rel="stylesheet" href="{{ '/assets/css/custom.css' | relative_url }}">


Stay updated with the latest in retirement planning, personal finance, and tax strategies.

## Personal Finance News by Topic

<div style="margin-bottom: 20px;">
  <button onclick="loadNews('retirement')" style="padding: 10px 20px; margin: 5px; cursor: pointer; background: #1e40af; color: white; border: none; border-radius: 50px; font-weight: 600;">Retirement</button>
  <button onclick="loadNews('personal-finance')" style="padding: 10px 20px; margin: 5px; cursor: pointer; background: #1e40af; color: white; border: none; border-radius: 50px; font-weight: 600;">Personal Finance</button>
  <button onclick="loadNews('tax')" style="padding: 10px 20px; margin: 5px; cursor: pointer; background: #1e40af; color: white; border: none; border-radius: 50px; font-weight: 600;">Tax</button>
</div>

<div id="news-feed" style="margin-top: 30px;">
  <p>Click a topic above to load news...</p>
</div>

<script>
// RSS feeds focused on retirement, personal finance, and tax
const newsFeeds = {
  'retirement': [
    'https://finance.yahoo.com/news/rssindex',
    'https://www.investing.com/rss/news_1.rss'
  ],
  'personal-finance': [
    'https://finance.yahoo.com/news/rssindex',
    'https://www.investing.com/rss/news_1.rss'
  ],
  'tax': [
    'https://finance.yahoo.com/news/rssindex',
    'https://www.investing.com/rss/news_1.rss'
  ]
};

async function loadNews(category) {
  const feedDiv = document.getElementById('news-feed');
  feedDiv.innerHTML = '<p>Loading news...</p>';
  
  const feeds = newsFeeds[category];
  let allItems = [];
  
  for (const feedUrl of feeds) {
    try {
      const response = await fetch(`https://api.rss2json.com/v1/api.json?rss_url=${encodeURIComponent(feedUrl)}`);
      const data = await response.json();
      
      if (data.items && data.items.length > 0) {
        allItems = allItems.concat(data.items.slice(0, 8));
      }
    } catch (error) {
      console.log('Feed failed:', feedUrl);
    }
  }
  
  if (allItems.length === 0) {
    feedDiv.innerHTML = '<p>Unable to load news at this time. Please try another category or refresh the page.</p>';
    return;
  }
  
  allItems.sort((a, b) => new Date(b.pubDate) - new Date(a.pubDate));
  allItems = allItems.slice(0, 12);
  
  let html = '<div style="max-width: 900px;">';
  allItems.forEach(item => {
    const description = item.description ? item.description.replace(/<[^>]*>/g, '').substring(0, 200) : '';
    html += `
      <div style="background: white; border-radius: 12px; padding: 1.5rem; margin-bottom: 1.5rem; box-shadow: 0 2px 12px rgba(0,0,0,0.06);">
        <h3 style="margin: 0 0 0.5rem 0;">
          <a href="${item.link}" target="_blank" style="color: #1e40af; text-decoration: none; font-family: 'Playfair Display', serif;">
            ${item.title}
          </a>
        </h3>
        <p style="color: #999; font-size: 0.9rem; margin: 0 0 0.75rem 0;">
          ${new Date(item.pubDate).toLocaleDateString()}
        </p>
        <p style="margin: 0; color: #666; line-height: 1.6;">
          ${description}...
        </p>
      </div>
    `;
  });
  html += '</div>';
  
  feedDiv.innerHTML = html;
}

window.onload = () => loadNews('retirement');
</script>

---

## Retirement Planning Calculator

<div style="background: #f8f9fa; padding: 2rem; border-radius: 12px; margin-top: 3rem; max-width: 600px;">
  <h3 style="margin-top: 0; font-family: 'Playfair Display', serif;">Quick Retirement Savings Goal</h3>
  
  <label style="display: block; margin-bottom: 0.5rem; font-weight: 500;">Current Age:</label>
  <input type="number" id="age" value="30" style="width: 100%; padding: 0.75rem; margin-bottom: 1rem; border: 2px solid #e5e7eb; border-radius: 12px;">
  
  <label style="display: block; margin-bottom: 0.5rem; font-weight: 500;">Retirement Age:</label>
  <input type="number" id="retireAge" value="65" style="width: 100%; padding: 0.75rem; margin-bottom: 1rem; border: 2px solid #e5e7eb; border-radius: 12px;">
  
  <label style="display: block; margin-bottom: 0.5rem; font-weight: 500;">Current Savings: $</label>
  <input type="number" id="savings" value="50000" style="width: 100%; padding: 0.75rem; margin-bottom: 1rem; border: 2px solid #e5e7eb; border-radius: 12px;">
  
  <label style="display: block; margin-bottom: 0.5rem; font-weight: 500;">Monthly Contribution: $</label>
  <input type="number" id="monthly" value="500" style="width: 100%; padding: 0.75rem; margin-bottom: 1rem; border: 2px solid #e5e7eb; border-radius: 12px;">
  
  <label style="display: block; margin-bottom: 0.5rem; font-weight: 500;">Expected Return: %</label>
  <input type="number" id="return" value="7" style="width: 100%; padding: 0.75rem; margin-bottom: 1rem; border: 2px solid #e5e7eb; border-radius: 12px;">
  
  <button onclick="calculate()" style="width: 100%; padding: 1rem; background: #1e40af; color: white; border: none; border-radius: 50px; font-weight: 600; cursor: pointer;">Calculate</button>
  
  <div id="result" style="margin-top: 1.5rem; font-size: 1.1rem;"></div>
</div>

<script>
function calculate() {
  const age = parseInt(document.getElementById('age').value);
  const retireAge = parseInt(document.getElementById('retireAge').value);
  const savings = parseFloat(document.getElementById('savings').value);
  const monthly = parseFloat(document.getElementById('monthly').value);
  const returnRate = parseFloat(document.getElementById('return').value) / 100 / 12;
  
  const years = retireAge - age;
  const months = years * 12;
  
  const futureValue = savings * Math.pow(1 + returnRate, months) + 
                     monthly * ((Math.pow(1 + returnRate, months) - 1) / returnRate);
  
  document.getElementById('result').innerHTML = 
    `<div style="background: white; padding: 1.5rem; border-radius: 12px; border: 2px solid #1e40af;">
      At age ${retireAge}, you'll have approximately:<br>
      <span style="color: #16a34a; font-size: 1.5rem; font-weight: 700;">$${futureValue.toLocaleString('en-US', {maximumFractionDigits: 0})}</span>
    </div>`;
}
</script>

---

*News sources: Yahoo Finance, Investing.com, and other financial news aggregators.*
