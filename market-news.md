---
layout: page
title: "Market News & Data"
permalink: /market-news/
---

## Today's Financial Headlines

<div id="rss-feed"></div>

<script>
fetch('https://api.rss2json.com/v1/api.json?rss_url=https://feeds.bloomberg.com/markets/news.rss')
  .then(response => response.json())
  .then(data => {
    let html = '<ul style="list-style-type: none; padding: 0;">';
    data.items.slice(0, 10).forEach(item => {
      html += `
        <li style="margin-bottom: 20px; padding-bottom: 20px; border-bottom: 1px solid #eee;">
          <h3 style="margin: 0;"><a href="${item.link}" target="_blank">${item.title}</a></h3>
          <p style="color: #666; font-size: 14px;">${new Date(item.pubDate).toLocaleString()}</p>
          <p>${item.description.substring(0, 200)}...</p>
        </li>
      `;
    });
    html += '</ul>';
    document.getElementById('rss-feed').innerHTML = html;
  })
  .catch(error => {
    document.getElementById('rss-feed').innerHTML = '<p>Unable to load news. Please refresh the page.</p>';
  });
</script>

---

## Live Market Data

<!-- TradingView Widget BEGIN -->
<div class="tradingview-widget-container">
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
      ],
      "originalTitle": "Indices"
    },
    {
      "title": "Commodities",
      "symbols": [
        {"s": "COMEX:GC1!", "d": "Gold"},
        {"s": "NYMEX:CL1!", "d": "Crude Oil"},
        {"s": "COMEX:SI1!", "d": "Silver"},
        {"s": "CBOT:ZC1!", "d": "Corn"}
      ],
      "originalTitle": "Commodities"
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
<!-- TradingView Widget END -->

---

*Market data updates automatically. News headlines refresh when you reload the page.*
