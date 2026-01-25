---
layout: page
title: Financial News
permalink: /market-news/
---

<link rel="stylesheet" href="{{ '/assets/css/custom.css' | relative_url }}">

Stay updated with the latest in retirement planning, personal finance, and tax strategies.

## Personal Finance News by Topic

<div style="margin-bottom: 20px;">
  <button onclick="loadNews('retirement')" id="btn-retirement" style="padding: 10px 20px; margin: 5px; cursor: pointer; background: #1e40af; color: white; border: none; border-radius: 50px; font-weight: 600;">Retirement</button>
  <button onclick="loadNews('personal-finance')" id="btn-personal-finance" style="padding: 10px 20px; margin: 5px; cursor: pointer; background: #64748b; color: white; border: none; border-radius: 50px; font-weight: 600;">Personal Finance</button>
  <button onclick="loadNews('tax')" id="btn-tax" style="padding: 10px 20px; margin: 5px; cursor: pointer; background: #64748b; color: white; border: none; border-radius: 50px; font-weight: 600;">Tax & Legal</button>
  <button onclick="loadNews('savings')" id="btn-savings" style="padding: 10px 20px; margin: 5px; cursor: pointer; background: #64748b; color: white; border: none; border-radius: 50px; font-weight: 600;">Savings & Banking</button>
</div>

<div id="news-feed" style="margin-top: 30px;">
  <p>Loading news...</p>
</div>

<script>
// Diverse RSS feeds focused on retirement, personal finance, tax, and savings
// Avoiding company-specific stock news
const newsFeeds = {
  'retirement': [
    'https://www.marketwatch.com/rss/realtimeheadlines',
    'https://finance.yahoo.com/news/rssindex',
    'https://www.kiplinger.com/feeds/rss/retirement-planning',
    'https://www.fool.com/feeds/index.aspx'
  ],
  'personal-finance': [
    'https://www.marketwatch.com/rss/realtimeheadlines',
    'https://finance.yahoo.com/news/rssindex',
    'https://www.nerdwallet.com/blog/feed/',
    'https://www.bankrate.com/feed/'
  ],
  'tax': [
    'https://www.marketwatch.com/rss/realtimeheadlines',
    'https://finance.yahoo.com/news/rssindex',
    'https://www.kiplinger.com/feeds/rss/tax-planning'
  ],
  'savings': [
    'https://www.marketwatch.com/rss/realtimeheadlines',
    'https://finance.yahoo.com/news/rssindex',
    'https://www.bankrate.com/feed/',
    'https://www.nerdwallet.com/blog/feed/'
  ]
};

// Keywords to filter content relevant to each category
const categoryKeywords = {
  'retirement': [
    'retirement', '401k', '401(k)', 'ira', 'roth', 'pension', 'social security',
    'medicare', 'early retirement', 'retire', 'retiring', 'retiree', 'nest egg',
    '403b', 'annuity', 'required minimum distribution', 'rmd', 'catch-up contribution'
  ],
  'personal-finance': [
    'budget', 'debt', 'credit card', 'mortgage', 'loan', 'financial planning',
    'estate planning', 'wealth', 'money management', 'financial advisor',
    'net worth', 'emergency fund', 'financial goals', 'spending', 'income',
    'financial health', 'credit score', 'bankruptcy', 'refinance'
  ],
  'tax': [
    'tax', 'irs', 'deduction', 'tax credit', 'filing', 'refund', 'withholding',
    'tax bracket', 'capital gains', 'tax law', 'tax reform', 'tax strategy',
    'tax planning', 'tax season', 'standard deduction', 'itemized', 'tax break',
    'tax rate', 'estate tax', 'gift tax', 'tax code'
  ],
  'savings': [
    'savings', 'savings account', 'high-yield', 'interest rate', 'cd', 'certificate of deposit',
    'money market', 'bank account', 'apy', 'fdic', 'online bank', 'savings rate',
    'emergency savings', 'bank promotion', 'bonus', 'treasury', 'i bond', 'series i'
  ]
};

// Keywords to EXCLUDE (company stocks, crypto, day trading)
const excludeKeywords = [
  'stock picks', 'buy this stock', 'stock alert', 'trading strategy',
  'day trading', 'options trading', 'penny stock', 'cryptocurrency', 'crypto',
  'bitcoin', 'ethereum', 'nft', 'forex', 'technical analysis', 'chart pattern'
];

function highlightActiveButton(category) {
  // Reset all buttons
  document.querySelectorAll('[id^="btn-"]').forEach(btn => {
    btn.style.background = '#64748b';
  });
  // Highlight active button
  const activeBtn = document.getElementById(`btn-${category}`);
  if (activeBtn) {
    activeBtn.style.background = '#1e40af';
  }
}

function isRelevantToCategory(item, category) {
  const text = (item.title + ' ' + (item.description || '')).toLowerCase();
  const keywords = categoryKeywords[category] || [];
  
  // Check if article should be excluded
  for (const exclude of excludeKeywords) {
    if (text.includes(exclude.toLowerCase())) {
      return false;
    }
  }
  
  // Check if article contains relevant keywords
  for (const keyword of keywords) {
    if (text.includes(keyword.toLowerCase())) {
      return true;
    }
  }
  
  return false;
}

async function loadNews(category) {
  const feedDiv = document.getElementById('news-feed');
  feedDiv.innerHTML = '<p>Loading news...</p>';
  
  highlightActiveButton(category);
  
  const feeds = newsFeeds[category];
  let allItems = [];
  
  for (const feedUrl of feeds) {
    try {
      const response = await fetch(`https://api.rss2json.com/v1/api.json?rss_url=${encodeURIComponent(feedUrl)}&count=20`);
      const data = await response.json();
      
      if (data.items && data.items.length > 0) {
        // Filter items based on category keywords
        const relevantItems = data.items.filter(item => isRelevantToCategory(item, category));
        allItems = allItems.concat(relevantItems);
      }
    } catch (error) {
      console.log('Feed failed:', feedUrl);
    }
  }
  
  if (allItems.length === 0) {
    feedDiv.innerHTML = `
      <div style="background: #fef3c7; border-left: 4px solid #f59e0b; padding: 1rem; border-radius: 8px;">
        <p style="margin: 0; color: #92400e;">
          <strong>No recent articles found for this category.</strong><br>
          Try another category or check back later. News sources may be temporarily unavailable.
        </p>
      </div>
    `;
    return;
  }
  
  // Remove duplicates based on title similarity
  const uniqueItems = [];
  const seenTitles = new Set();
  
  for (const item of allItems) {
    const normalizedTitle = item.title.toLowerCase().substring(0, 50);
    if (!seenTitles.has(normalizedTitle)) {
      seenTitles.add(normalizedTitle);
      uniqueItems.push(item);
    }
  }
  
  // Sort by date and limit
  uniqueItems.sort((a, b) => new Date(b.pubDate) - new Date(a.pubDate));
  const displayItems = uniqueItems.slice(0, 12);
  
  let html = '<div style="max-width: 900px;">';
  displayItems.forEach(item => {
    const description = item.description ? item.description.replace(/<[^>]*>/g, '').substring(0, 200) : '';
    const source = new URL(item.link).hostname.replace('www.', '');
    
    html += `
      <div style="background: white; border-radius: 12px; padding: 1.5rem; margin-bottom: 1.5rem; box-shadow: 0 2px 12px rgba(0,0,0,0.06); transition: box-shadow 0.2s;" onmouseover="this.style.boxShadow='0 4px 20px rgba(0,0,0,0.12)'" onmouseout="this.style.boxShadow='0 2px 12px rgba(0,0,0,0.06)'">
        <h3 style="margin: 0 0 0.5rem 0;">
          <a href="${item.link}" target="_blank" rel="noopener noreferrer" style="color: #1e40af; text-decoration: none; font-family: 'Playfair Display', serif;">
            ${item.title}
          </a>
        </h3>
        <p style="color: #999; font-size: 0.9rem; margin: 0 0 0.75rem 0;">
          ${new Date(item.pubDate).toLocaleDateString('en-US', { month: 'short', day: 'numeric', year: 'numeric' })} • ${source}
        </p>
        <p style="margin: 0; color: #666; line-height: 1.6;">
          ${description}${description ? '...' : ''}
        </p>
      </div>
    `;
  });
  html += '</div>';
  
  feedDiv.innerHTML = html;
}

// Load retirement news by default on page load
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

<div style="background: #f1f5f9; padding: 1rem; border-radius: 8px; margin-top: 2rem; font-size: 0.9rem; color: #64748b;">
  <p style="margin: 0;"><strong>News Sources:</strong> MarketWatch, Yahoo Finance, Kiplinger, NerdWallet, Bankrate, and The Motley Fool. Articles are automatically filtered to focus on retirement, personal finance, tax planning, and savings strategies relevant to our audience.</p>
</div>
