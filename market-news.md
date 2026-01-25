---
layout: page
title: Financial News
permalink: /market-news/
---

<link rel="stylesheet" href="{{ '/assets/css/custom.css' | relative_url }}">

Stay updated with the latest in retirement planning, personal finance, and tax strategies.

## Latest Financial News

<div id="news-feed" style="margin-top: 30px;">
  <p>Loading news...</p>
</div>

<script>
// Using Google News RSS feeds which are more reliable
const NEWS_FEEDS = [
  'https://news.google.com/rss/search?q=retirement+planning+401k+IRA&hl=en-US&gl=US&ceid=US:en',
  'https://news.google.com/rss/search?q=personal+finance+tax+savings&hl=en-US&gl=US&ceid=US:en',
  'https://news.google.com/rss/search?q=social+security+medicare&hl=en-US&gl=US&ceid=US:en',
  'https://news.google.com/rss/search?q=high+yield+savings+bank+rates&hl=en-US&gl=US&ceid=US:en'
];

async function fetchGoogleNewsRSS(url) {
  try {
    // Use rss2json API without key (limited but works)
    const apiUrl = `https://api.rss2json.com/v1/api.json?rss_url=${encodeURIComponent(url)}`;
    
    const response = await fetch(apiUrl);
    if (!response.ok) return [];
    
    const data = await response.json();
    if (data.status !== 'ok' || !data.items) return [];
    
    return data.items.map(item => ({
      title: item.title || '',
      link: item.link || '',
      description: (item.description || '').replace(/<[^>]*>/g, '').substring(0, 200),
      pubDate: item.pubDate || new Date().toISOString(),
      source: item.author || 'Google News'
    })).filter(article => article.title && article.link);
    
  } catch (error) {
    console.error('Error fetching feed:', error);
    return [];
  }
}

function isRelevantArticle(article) {
  const text = (article.title + ' ' + article.description).toLowerCase();
  
  // Exclude unwanted content
  const excludeTerms = [
    'stock to buy', 'stocks to buy', 'buy this stock', 'crypto', 'bitcoin', 
    'ethereum', 'nft', 'forex', 'penny stock', 'trading alert'
  ];
  
  for (const term of excludeTerms) {
    if (text.includes(term)) return false;
  }
  
  return true;
}

async function loadNews() {
  const feedDiv = document.getElementById('news-feed');
  feedDiv.innerHTML = '<p style="color: #64748b;"><em>Loading latest financial news from Google News...</em></p>';
  
  let allArticles = [];
  
  // Fetch from all feeds
  for (const feedUrl of NEWS_FEEDS) {
    const articles = await fetchGoogleNewsRSS(feedUrl);
    allArticles = allArticles.concat(articles);
  }
  
  console.log(`Fetched ${allArticles.length} articles from Google News`);
  
  // Filter relevant articles
  let filteredArticles = allArticles.filter(article => isRelevantArticle(article));
  
  // Remove duplicates
  const seen = new Set();
  filteredArticles = filteredArticles.filter(article => {
    const key = article.title.toLowerCase().substring(0, 50);
    if (seen.has(key)) return false;
    seen.add(key);
    return true;
  });
  
  // Sort by date
  filteredArticles.sort((a, b) => new Date(b.pubDate) - new Date(a.pubDate));
  
  // Limit to 20 articles
  filteredArticles = filteredArticles.slice(0, 20);
  
  if (filteredArticles.length === 0) {
    feedDiv.innerHTML = `
      <div style="background: #fef3c7; border-left: 4px solid #f59e0b; padding: 1rem; border-radius: 8px;">
        <p style="margin: 0; color: #92400e;">
          <strong>Unable to load news at this time.</strong><br>
          Please try refreshing the page. If the issue persists, news feeds may be temporarily unavailable.
        </p>
      </div>
    `;
    return;
  }
  
  // Display articles
  let html = '<div style="max-width: 900px;">';
  
  filteredArticles.forEach(article => {
    const displayDate = new Date(article.pubDate).toLocaleDateString('en-US', { 
      month: 'short', 
      day: 'numeric', 
      year: 'numeric' 
    });
    
    html += `
      <div style="background: white; border-radius: 12px; padding: 1.5rem; margin-bottom: 1.5rem; box-shadow: 0 2px 12px rgba(0,0,0,0.06); transition: box-shadow 0.2s;" onmouseover="this.style.boxShadow='0 4px 20px rgba(0,0,0,0.12)'" onmouseout="this.style.boxShadow='0 2px 12px rgba(0,0,0,0.06)'">
        <h3 style="margin: 0 0 0.5rem 0;">
          <a href="${article.link}" target="_blank" rel="noopener noreferrer" style="color: #1e40af; text-decoration: none; font-family: 'Playfair Display', serif;">
            ${article.title}
          </a>
        </h3>
        <p style="color: #999; font-size: 0.9rem; margin: 0 0 0.75rem 0;">
          ${displayDate}${article.source ? ' • ' + article.source : ''}
        </p>
        <p style="margin: 0; color: #666; line-height: 1.6;">
          ${article.description}${article.description.length >= 200 ? '...' : ''}
        </p>
      </div>
    `;
  });
  html += '</div>';
  
  feedDiv.innerHTML = html;
}

// Load news on page load
window.onload = () => loadNews();
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

<div style="background: #f1f5f9; padding: 1rem; border-radius: 8px; margin-top: 2rem; font-size: 0.9rem; color: #64748b;">
  <p style="margin: 0;"><strong>News Source:</strong> Articles automatically pulled from Google News with search filters for retirement planning, personal finance, tax strategies, and savings topics.</p>
  <p style="margin: 0.5rem 0 0 0;"><em>Content updates automatically each time you visit the page. Stock picks and cryptocurrency content are filtered out.</em></p>
</div>
