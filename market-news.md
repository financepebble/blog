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
// Multiple diverse RSS feed sources for financial news
const RSS_FEEDS = [
  // Major financial news (broader coverage)
  { url: 'https://finance.yahoo.com/news/rssindex', name: 'Yahoo Finance' },
  { url: 'https://www.marketwatch.com/rss/topstories', name: 'MarketWatch' },
  
  // Personal finance & retirement focused
  { url: 'https://feeds.aarp.org/aarp/retirement.xml', name: 'AARP Retirement' },
  { url: 'https://www.kiplinger.com/fronts/rss/all/index.rss', name: 'Kiplinger' },
  
  // Banking & savings
  { url: 'https://www.bankrate.com/feed/', name: 'Bankrate' },
  { url: 'https://www.nerdwallet.com/blog/feed/', name: 'NerdWallet' },
  
  // Financial education
  { url: 'https://www.investopedia.com/feedbuilder/feed/getfeed?feedName=rss_headline', name: 'Investopedia' }
];

// Fallback curated content (used if RSS feeds fail)
const FALLBACK_NEWS = [
  {
    title: "2026 Retirement Account Contribution Limits Increased",
    description: "The IRS announced higher contribution limits for 401(k), IRA, and other retirement accounts for 2026. Workers under 50 can contribute up to $23,500 to 401(k) plans, while catch-up contributions for those 50+ increased to $7,500.",
    link: "https://www.irs.gov/retirement-plans/plan-participant-employee/retirement-topics-401k-and-profit-sharing-plan-contribution-limits",
    pubDate: "2026-01-20",
    source: "IRS"
  },
  {
    title: "High-Yield Savings Accounts Still Offering Over 4% APY",
    description: "Despite market volatility, several online banks continue offering competitive savings rates above 4% APY. Financial experts recommend comparing rates quarterly as the Fed evaluates monetary policy.",
    link: "https://www.bankrate.com/banking/savings/rates/",
    pubDate: "2026-01-18",
    source: "Bankrate"
  },
  {
    title: "Tax Brackets Adjusted for Inflation in 2026",
    description: "The IRS released updated federal income tax brackets for 2026, with inflation adjustments benefiting most taxpayers. The standard deduction also increased to $16,100 for single filers and $32,200 for married couples filing jointly.",
    link: "https://www.irs.gov/newsroom/irs-provides-tax-inflation-adjustments-for-tax-year-2026",
    pubDate: "2026-01-15",
    source: "IRS"
  },
  {
    title: "Social Security COLA Increase Takes Effect",
    description: "Over 71 million Americans will see a cost-of-living adjustment in their Social Security benefits this year. Understanding how COLA affects retirement income is crucial for financial planning.",
    link: "https://www.ssa.gov/cola/",
    pubDate: "2026-01-12",
    source: "Social Security Administration"
  },
  {
    title: "Medicare Part B Premium Changes for 2026",
    description: "The standard Medicare Part B premium has been announced for 2026. High-income beneficiaries should review IRMAA thresholds to understand their potential premium adjustments.",
    link: "https://www.medicare.gov/your-medicare-costs/part-b-costs",
    pubDate: "2026-01-10",
    source: "Medicare.gov"
  },
  {
    title: "Series I Bonds: Are They Still Worth Buying?",
    description: "Treasury I Bonds continue to offer inflation protection with rates adjusting semi-annually. Financial planners weigh in on whether these securities still make sense for conservative investors.",
    link: "https://www.treasurydirect.gov/savings-bonds/i-bonds/",
    pubDate: "2026-01-08",
    source: "TreasuryDirect"
  },
  {
    title: "Health Savings Account Limits Rise for 2026",
    description: "HSA contribution limits increased to $4,300 for individuals and $8,550 for families in 2026. These tax-advantaged accounts remain powerful tools for retirement healthcare planning.",
    link: "https://www.irs.gov/publications/p969",
    pubDate: "2026-01-05",
    source: "IRS"
  },
  {
    title: "Estate Tax Exemption Reaches $15 Million Per Person",
    description: "The federal estate tax exemption continues climbing with inflation adjustments. Estate planning professionals recommend reviewing strategies given potential future tax law changes.",
    link: "https://www.irs.gov/businesses/small-businesses-self-employed/estate-tax",
    pubDate: "2026-01-03",
    source: "IRS"
  },
  {
    title: "Credit Card Interest Rates Hit Record Highs",
    description: "Average credit card APRs exceed 21%, prompting financial experts to recommend aggressive debt paydown strategies including balance transfers and the avalanche method.",
    link: "https://www.nerdwallet.com/article/credit-cards/credit-card-interest-rate",
    pubDate: "2025-12-28",
    source: "NerdWallet"
  },
  {
    title: "Required Minimum Distribution Rules Updated",
    description: "New RMD regulations affect retirees with traditional IRAs and 401(k)s. Understanding when withdrawals must begin is critical to avoid hefty IRS penalties.",
    link: "https://www.irs.gov/retirement-plans/plan-participant-employee/retirement-topics-required-minimum-distributions-rmds",
    pubDate: "2025-12-22",
    source: "IRS"
  },
  {
    title: "Bank Account Bonuses: Top Offers for Early 2026",
    description: "Major banks are offering cash bonuses ranging from $200 to $500 for new checking and savings accounts. Compare requirements carefully before opening accounts solely for bonuses.",
    link: "https://www.bankrate.com/banking/bank-promotions/",
    pubDate: "2025-12-20",
    source: "Bankrate"
  },
  {
    title: "Enhanced Catch-Up Contributions for Ages 60-63",
    description: "Workers aged 60-63 can now make super catch-up contributions to 401(k) plans up to $11,250 for 2026, significantly boosting late-career retirement savings potential.",
    link: "https://www.irs.gov/retirement-plans/plan-participant-employee/retirement-topics-catch-up-contributions",
    pubDate: "2025-12-15",
    source: "IRS"
  }
];

function parseRSSItem(item) {
  const getElementText = (element, tagName) => {
    const el = element.getElementsByTagName(tagName)[0];
    return el ? (el.textContent || el.innerText || '').trim() : '';
  };
  
  return {
    title: getElementText(item, 'title'),
    link: getElementText(item, 'link'),
    description: getElementText(item, 'description').replace(/<[^>]*>/g, '').trim(),
    pubDate: getElementText(item, 'pubDate'),
    source: ''
  };
}

async function fetchRSSFeed(feedObj) {
  const { url, name } = feedObj;
  
  try {
    // Multiple CORS proxy options
    const proxies = [
      `https://api.allorigins.win/raw?url=${encodeURIComponent(url)}`,
      `https://corsproxy.io/?${encodeURIComponent(url)}`,
      `https://api.codetabs.com/v1/proxy?quest=${encodeURIComponent(url)}`
    ];
    
    for (const proxyUrl of proxies) {
      try {
        const controller = new AbortController();
        const timeoutId = setTimeout(() => controller.abort(), 5000); // 5 second timeout
        
        const response = await fetch(proxyUrl, { signal: controller.signal });
        clearTimeout(timeoutId);
        
        if (!response.ok) continue;
        
        const text = await response.text();
        const parser = new DOMParser();
        const xml = parser.parseFromString(text, 'text/xml');
        
        // Check for parsing errors
        const parserError = xml.getElementsByTagName('parsererror');
        if (parserError.length > 0) continue;
        
        const items = xml.getElementsByTagName('item');
        const articles = [];
        
        for (let i = 0; i < Math.min(items.length, 10); i++) {
          const article = parseRSSItem(items[i]);
          if (article.title && article.link) {
            article.source = name;
            articles.push(article);
          }
        }
        
        if (articles.length > 0) {
          console.log(`✓ Fetched ${articles.length} articles from ${name}`);
          return articles;
        }
      } catch (e) {
        if (e.name === 'AbortError') {
          console.log(`⏱ Timeout fetching ${name}`);
        }
        continue;
      }
    }
    
    console.log(`✗ All proxies failed for ${name}`);
    return [];
  } catch (error) {
    console.log(`✗ Error fetching ${name}:`, error.message);
    return [];
  }
}

function isRelevantArticle(article) {
  const text = (article.title + ' ' + article.description).toLowerCase();
  
  // AGGRESSIVE EXCLUSIONS - reject stock picks, company analysis, crypto
  const excludeTerms = [
    // Crypto
    'cryptocurrency', 'crypto', 'bitcoin', 'ethereum', 'nft', 'blockchain', 'chainlink',
    'dogecoin', 'ripple', 'cardano',
    
    // Stock-specific language
    'stock to buy', 'stocks to buy', 'buy this stock', 'stock alert', 'stock pick',
    'better buy', 'stock while', 'vs.', 'stock up', 'stock down', 'buy right now',
    'dividend stock', 'share', 'shares', 'market share', 'stock yielding',
    'etf to buy', 'better long-term play', 'still a buy', 'great buys',
    
    // Trading/investment language
    'trading', 'trader', 'day trade', 'options', 'penny stock', 'forex',
    'technical analysis', 'chart pattern', 'momentum', 'hedge fund',
    
    // Individual companies (common stock picks)
    'walmart', 'target', 'amazon', 'apple', 'tesla', 'nvidia', 'microsoft',
    'oracle', 'intel', 'micron', 'rocket lab', 'energy transfer',
    
    // Investment jargon
    'voog', 'iwo', 'quantum computing stocks', 'ai stock', 'semiconductor',
    'billionaire', 'hedge fund', 'portfolio'
  ];
  
  // Check exclusions
  for (const term of excludeTerms) {
    if (text.includes(term)) {
      return false;
    }
  }
  
  // Must match at least one relevant keyword for personal finance
  const relevantKeywords = [
    // Retirement
    'retirement', '401k', '401(k)', 'ira', 'roth', 'pension', 'social security', 
    'medicare', 'rmd', 'annuity', 'retiree', 'catch-up',
    
    // Tax
    'tax', 'irs', 'deduction', 'refund', 'filing', 'bracket', 'estate tax', 
    'gift tax', 'tax credit', 'withholding', 'tax planning',
    
    // Savings & Banking
    'savings account', 'bank account', 'interest rate', 'apy', 'cd', 
    'certificate of deposit', 'bond', 'i bond', 'treasury', 'high-yield', 
    'money market', 'emergency fund',
    
    // Personal Finance
    'personal finance', 'budget', 'budgeting', 'debt', 'mortgage', 'loan', 
    'credit card', 'credit score', 'financial planning', 'estate planning',
    'hsa', 'health savings'
  ];
  
  return relevantKeywords.some(keyword => text.includes(keyword));
}

async function loadNews() {
  const feedDiv = document.getElementById('news-feed');
  feedDiv.innerHTML = '<p style="color: #64748b;"><em>Loading latest financial news...</em></p>';
  
  let allArticles = [];
  let successCount = 0;
  
  // Try to fetch from RSS feeds
  const fetchPromises = RSS_FEEDS.map(feed => fetchRSSFeed(feed));
  const results = await Promise.all(fetchPromises);
  
  results.forEach(articles => {
    if (articles.length > 0) {
      successCount++;
      allArticles = allArticles.concat(articles);
    }
  });
  
  console.log(`Successfully fetched from ${successCount}/${RSS_FEEDS.length} feeds`);
  console.log(`Total articles from RSS: ${allArticles.length}`);
  
  // If we got fewer than 5 articles, use fallback content
  if (allArticles.length < 5) {
    console.log('Using fallback curated content');
    allArticles = FALLBACK_NEWS.slice();
  }
  
  // Filter for relevant content
  let filteredArticles = allArticles.filter(article => isRelevantArticle(article));
  
  console.log(`After filtering: ${filteredArticles.length} relevant articles`);
  
  // Remove duplicates based on title
  const seen = new Set();
  filteredArticles = filteredArticles.filter(article => {
    const key = article.title.toLowerCase().substring(0, 50);
    if (seen.has(key)) return false;
    seen.add(key);
    return true;
  });
  
  // Sort by date
  filteredArticles.sort((a, b) => {
    const dateA = new Date(a.pubDate || '2025-01-01');
    const dateB = new Date(b.pubDate || '2025-01-01');
    return dateB - dateA;
  });
  
  // Limit to 15 articles
  filteredArticles = filteredArticles.slice(0, 15);
  
  if (filteredArticles.length === 0) {
    feedDiv.innerHTML = `
      <div style="background: #fef3c7; border-left: 4px solid #f59e0b; padding: 1rem; border-radius: 8px;">
        <p style="margin: 0; color: #92400e;">
          <strong>No relevant articles found.</strong><br>
          Please check back later for updates on retirement, taxes, and personal finance.
        </p>
      </div>
    `;
    return;
  }
  
  // Display articles
  let html = '<div style="max-width: 900px;">';
  
  // Add indicator if using fallback
  if (successCount === 0) {
    html += `
      <div style="background: #e0f2fe; border-left: 4px solid #0284c7; padding: 0.75rem; margin-bottom: 1.5rem; border-radius: 8px; font-size: 0.9rem;">
        <p style="margin: 0; color: #075985;">
          📰 <strong>Showing curated news highlights.</strong> Live feeds will resume when available.
        </p>
      </div>
    `;
  }
  
  filteredArticles.forEach(article => {
    const description = article.description.substring(0, 200);
    const displayDate = article.pubDate ? 
      new Date(article.pubDate).toLocaleDateString('en-US', { month: 'short', day: 'numeric', year: 'numeric' }) :
      'Recent';
    
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
          ${description}${description.length >= 200 ? '...' : ''}
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
  <p style="margin: 0;"><strong>News Sources:</strong> Yahoo Finance, MarketWatch, AARP, Kiplinger, Bankrate, NerdWallet, and Investopedia. Articles are automatically filtered to focus on retirement planning, personal finance, tax strategies, and savings topics relevant to our 40-60 year old audience.</p>
  <p style="margin: 0.5rem 0 0 0;"><em>Content automatically updates when available, with curated fallback for reliability. Stock picks and cryptocurrency news are excluded.</em></p>
</div>
