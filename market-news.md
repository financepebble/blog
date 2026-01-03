---
layout: page
title: "Market News & Data"
permalink: /market-news/
---

## Financial News by Category

<div style="margin-bottom: 20px;">
  <button onclick="loadNews('business')" style="padding: 10px 20px; margin: 5px; cursor: pointer;">Business</button>
  <button onclick="loadNews('stocks')" style="padding: 10px 20px; margin: 5px; cursor: pointer;">Stock Market</button>
  <button onclick="loadNews('crypto')" style="padding: 10px 20px; margin: 5px; cursor: pointer;">Cryptocurrency</button>
  <button onclick="loadNews('economy')" style="padding: 10px 20px; margin: 5px; cursor: pointer;">Economy</button>
  <button onclick="loadNews('technology')" style="padding: 10px 20px; margin: 5px; cursor: pointer;">Tech & Finance</button>
</div>

<div id="news-feed" style="margin-top: 30px;">
  <p>Click a category above to load news...</p>
</div>

<script>
// Multiple free, non-paywalled RSS feeds
const newsFeeds = {
  business: [
    'https://feeds.marketwatch.com/marketwatch/topstories/',
    'https://www.cnbc.com/id/100003114/device/rss/rss.html',
    'https://finance.yahoo.com/news/rssindex'
  ],
  stocks: [
    'https://feeds.marketwatch.com/marketwatch/marketpulse/',
    'https://www.investing.com/rss/news.rss'
  ],
  crypto: [
    'https://cointelegraph.com/rss',
    'https://decrypt.co/feed'
  ],
  economy: [
    'https://www.investing.com/rss/news_285.rss',
    'https://feeds.marketwatch.com/marketwatch/economy/'
  ],
  technology: [
    'https://techcrunch.com/tag/fintech/feed/',
    'https://www.theverge.com/rss/index.xml'
  ]
};

async function loadNews(category) {
  const feedDiv = document.getElementById('news-feed');
  feedDiv.innerHTML = '<p>Loading news...</p>';
  
  const feeds = newsFeeds[category];
  let allItems = [];
  
  // Try each feed in the category
  for (const feedUrl of feeds) {
    try {
      const response = await fetch(`https://api.rss2json.com/v1/api.json?rss_url=${encodeURIComponent(feedUrl)}`);
      const data = await response.json();
      
      if (data.items && data.items.length > 0) {
        allItems = allItems.concat(data.items.slice(0, 5));
      }
    } catch (error) {
      console.log('Feed failed:', feedUrl);
    }
  }
  
  if (allItems.length === 0) {
    feedDiv.innerHTML = '<p>Unable to load news. Please try another category or refresh the page.</p>';
    return;
  }
  
  // Sort by date and take top 10
  allItems.sort((a, b) => new Date(b.pubDate) - new Date(a.pubDate));
  allItems = allItems.slice(0, 10);
  
  let html = '<div style="max-width: 900px;">';
  allItems.forEach(item => {
    const description = item.description ? item.description.replace(/<[^>]*>/g, '').substring(0, 250) : '';
    html += `
      <div style="margin-bottom: 25px; padding-bottom: 25px; border-bottom: 1px solid #ddd;">
        <h3 style="margin: 0 0 8px 0;">
          <a href="${item.link}" target="_blank" style="color: #2563eb; text-decoration: none;">
            ${item.title}
          </a>
        </h3>
        <p style="color: #666; font-size: 13px; margin: 0 0 10px 0;">
          ${new Date(item.pubDate).toLocaleString()} • ${item.author || 'News'}
        </p>
        <p style="margin: 0; color: #333;">
          ${description}...
        </p>
      </div>
    `;
  });
  html += '</div>';
  
  feedDiv.innerHTML = html;
}

// Auto-load business news on page load
window.onload = () => loadNews('business');
</script>

---

## Live Market Data

<!-- TradingView Widget -->
<div class="tradingview-widget-container" style="margin-top: 40px;">
  <div class="tradingview-widget-container__widget"></div>
  <script type="text/javascript" src="https://s3.tradingview.com/external-embedding/embed-widget-market-overview.js" async>
  {
  "colorTheme": "light",
  "dateRange": "1D",
  "showChart": true,
  "locale": "en",
  "width": "100%",
  "height": "600",
  "largeChartUrl": "",
  "isTransparent": false,
  "showSymbolLogo": true,
  "showFloatingTooltip": false,
  "plotLineColorGrowing": "rgba(41, 98, 255, 1)",
  "plotLineColorFalling": "rgba(41, 98, 255, 1)",
  "gridLineColor": "rgba(240, 243, 250, 0)",
  "scaleFontColor": "rgba(106, 109, 120, 1)",
  "belowLineFillColorGrowing": "rgba(41, 98, 255, 0.12)",
  "belowLineFillColorFalling": "rgba(41, 98, 255, 0.12)",
  "belowLineFillColorGrowingBottom": "rgba(41, 98, 255, 0)",
  "belowLineFillColorFallingBottom": "rgba(41, 98, 255, 0)",
  "symbolActiveColor": "rgba(41, 98, 255, 0.12)",
  "tabs": [
    {
      "title": "Indices",
      "symbols": [
        {"s": "FOREXCOM:SPXUSD", "d": "S&P 500"},
        {"s": "FOREXCOM:NSXUSD", "d": "Nasdaq 100"},
        {"s": "FOREXCOM:DJI", "d": "Dow 30"},
        {"s": "INDEX:NKY", "d": "Nikkei 225"},
        {"s": "CURRENCYCOM:UK100", "d": "FTSE 100"}
      ]
    },
    {
      "title": "Commodities",
      "symbols": [
        {"s": "COMEX:GC1!", "d": "Gold"},
        {"s": "NYMEX:CL1!", "d": "Crude Oil"},
        {"s": "COMEX:SI1!", "d": "Silver"}
      ]
    },
    {
      "title": "Crypto",
      "symbols": [
        {"s": "BINANCE:BTCUSDT", "d": "Bitcoin"},
        {"s": "BINANCE:ETHUSDT", "d": "Ethereum"},
        {"s": "BINANCE:SOLUSDT", "d": "Solana"}
      ]
    }
  ]
}
  </script>
</div>

---

*News sources: MarketWatch, CNBC, Yahoo Finance, Investing.com, CoinTelegraph, Decrypt, TechCrunch. Market data from TradingView.*
