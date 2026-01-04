---
layout: page
title: Financial News
permalink: /market-news/
---

# Financial News & Market Data

Stay updated with the latest in retirement planning, personal finance, and tax strategies.

## Personal Finance News by Topic

<div style="margin-bottom: 20px;">
  <button onclick="loadNews('retirement')" class="btn" style="margin: 5px;">Retirement</button>
  <button onclick="loadNews('personal-finance')" class="btn" style="margin: 5px;">Personal Finance</button>
  <button onclick="loadNews('tax')" class="btn" style="margin: 5px;">Tax</button>
</div>

<div id="news-feed" style="margin-top: 30px;">
  <p>Click a topic above to load news...</p>
</div>

<script>
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
  
  let html = '<div style="display: grid; grid-template-columns: repeat(auto-fill, minmax(350px, 1fr)); gap: 1.5rem; margin-top: 2rem;">';
  allItems.forEach(item => {
    const description = item.description ? item.description.replace(/<[^>]*>/g, '').substring(0, 200) : '';
    html += `
      <div style="background: white; border-radius: 16px; padding: 2rem; box-shadow: 0 2px 12px rgba(0,0,0,0.06); transition: all 0.3s;" onmouseover="this.style.transform='translateY(-4px)'; this.style.boxShadow='0 8px 24px rgba(0,0,0,0.12)'" onmouseout="this.style.transform='translateY(0)'; this.style.boxShadow='0 2px 12px rgba(0,0,0,0.06)'">
        <h3 style="margin: 0 0 0.75rem 0; font-family: 'Playfair Display', serif; font-size: 1.3rem; line-height: 1.4;">
          <a href="${item.link}" target="_blank" style="color: #1a1a1a; text-decoration: none;">
            ${item.title}
          </a>
        </h3>
        <p style="color: #999; font-size: 0.9rem; margin: 0 0 1rem 0;">
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

<div style="background: linear-gradient(135deg, #eff6ff, #dbeafe); padding: 2rem; border-radius: 16px; margin-top: 3rem; max-width: 600px; box-shadow: 0 2px 12px rgba(0,0,0,0.06);">
  <h3 style="margin-top: 0; font-family: 'Playfair Display', serif; color: #1e40af;">Quick Retirement Savings Goal</h3>
  
  <label style="display: block; margin-bottom: 0.5rem; font-weight: 500;">Current Age:</label>
  <input type="number" id="age" value="30" style="width: 100%; padding: 1rem; margin-bottom: 1rem; border: 2px solid #e5e7eb; border-radius: 12px; font-family: 'Inter', sans-serif;">
  
  <label style="display: block; margin-bottom: 0.5rem; font-weight: 500;">Retirement Age:</label>
  <input type="number" id="retireAge" value="65" style="width: 100%; padding: 1rem; margin-bottom: 1rem; border: 2px solid #e5e7eb; border-radius: 12px; font-family: 'Inter', sans-serif;">
  
  <label style="display: block; margin-bottom: 0.5rem; font-weight: 500;">Current Savings: $</label>
  <input type="number" id="savings" value="50000" style="width: 100%; padding: 1rem; margin-bottom: 1rem; border: 2px solid #e5e7eb; border-radius: 12px; font-family: 'Inter', sans-serif;">
  
  <label style="display: block; margin-bottom: 0.5rem; font-weight: 500;">Monthly Contribution: $</label>
  <input type="number" id="monthly" value="500" style="width: 100%; padding: 1rem; margin-bottom: 1rem; border: 2px solid #e5e7eb; border-radius: 12px; font-family: 'Inter', sans-serif;">
  
  <label style="display: block; margin-bottom: 0.5rem; font-weight: 500;">Expected Return: %</label>
  <input type="number" id="return" value="7" style="width: 100%; padding: 1rem; margin-bottom: 1.5rem; border: 2px solid #e5e7eb; border-radius: 12px; font-family: 'Inter', sans-serif;">
  
  <button onclick="calculate()" class="btn" style="width: 100%;">Calculate My Timeline</button>
  
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
    `<div style="background: white; padding: 1.5rem; border-radius: 12px; border-left: 4px solid #1e40af; box-shadow: 0 2px 8px rgba(0,0,0,0.05);">
      <p style="margin: 0 0 0.5rem 0;">At age <strong>${retireAge}</strong>, you'll have approximately:</p>
      <p style="margin: 0; font-size: 2rem; color: #16a34a; font-weight: 700; font-family: 'Playfair Display', serif;">$${futureValue.toLocaleString('en-US', {maximumFractionDigits: 0})}</p>
    </div>`;
}
</script>

---

<div class="info-box">
  <p style="margin: 0;"><strong>📊 News Sources:</strong> Yahoo Finance, Investing.com, and other financial news aggregators. Content refreshes automatically.</p>
</div>
