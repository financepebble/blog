---
layout: page
title: "Financial News"
permalink: /market-news/
---

## Personal Finance News

### Latest Retirement News
<iframe src="https://news.google.com/rss/search?q=retirement+planning+401k&hl=en-US&gl=US&ceid=US:en" 
        style="display:none;" 
        onload="loadGoogleNews(this, 'retirement-news')"></iframe>
<div id="retirement-news">Loading retirement news...</div>

---

### Latest Personal Finance News
<iframe src="https://news.google.com/rss/search?q=personal+finance+savings+budgeting&hl=en-US&gl=US&ceid=US:en" 
        style="display:none;" 
        onload="loadGoogleNews(this, 'finance-news')"></iframe>
<div id="finance-news">Loading personal finance news...</div>

---

### Latest Tax News
<iframe src="https://news.google.com/rss/search?q=tax+planning+IRS+income+tax&hl=en-US&gl=US&ceid=US:en" 
        style="display:none;" 
        onload="loadGoogleNews(this, 'tax-news')"></iframe>
<div id="tax-news">Loading tax news...</div>

<script>
async function loadGoogleNews(iframe, targetId) {
  const url = iframe.src;
  try {
    const response = await fetch(`https://api.rss2json.com/v1/api.json?rss_url=${encodeURIComponent(url)}`);
    const data = await response.json();
    
    if (data.items && data.items.length > 0) {
      let html = '';
      data.items.slice(0, 8).forEach(item => {
        const description = item.description ? item.description.replace(/<[^>]*>/g, '').substring(0, 150) : '';
        html += `
          <div style="margin-bottom: 20px; padding-bottom: 20px; border-bottom: 1px solid #ddd;">
            <h4 style="margin: 0 0 5px 0;">
              <a href="${item.link}" target="_blank" style="color: #2563eb; text-decoration: none;">
                ${item.title}
              </a>
            </h4>
            <p style="color: #666; font-size: 12px; margin: 0 0 8px 0;">
              ${new Date(item.pubDate).toLocaleDateString()}
            </p>
            <p style="margin: 0; color: #333;">
              ${description}...
            </p>
          </div>
        `;
      });
      document.getElementById(targetId).innerHTML = html;
    } else {
      document.getElementById(targetId).innerHTML = '<p>No news available at this time.</p>';
    }
  } catch (error) {
    document.getElementById(targetId).innerHTML = '<p>Unable to load news. Please refresh the page.</p>';
  }
}
</script>

---

## Retirement Planning Calculator

<div style="background: #f8f9fa; padding: 20px; border-radius: 8px; margin-top: 30px; max-width: 600px;">
  <h3 style="margin-top: 0;">Quick Retirement Savings Goal</h3>
  
  <label>Current Age: <input type="number" id="age" value="30" style="width: 80px; padding: 5px;"></label><br><br>
  <label>Retirement Age: <input type="number" id="retireAge" value="65" style="width: 80px; padding: 5px;"></label><br><br>
  <label>Current Savings: $<input type="number" id="savings" value="50000" style="width: 120px; padding: 5px;"></label><br><br>
  <label>Monthly Contribution: $<input type="number" id="monthly" value="500" style="width: 120px; padding: 5px;"></label><br><br>
  <label>Expected Return: <input type="number" id="return" value="7" style="width: 60px; padding: 5px;">%</label><br><br>
  
  <button onclick="calculate()" style="padding: 10px 30px; background: #2563eb; color: white; border: none; border-radius: 5px; cursor: pointer;">Calculate</button>
  
  <div id="result" style="margin-top: 20px; font-size: 18px; font-weight: bold;"></div>
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
    `At age ${retireAge}, you'll have approximately:<br><span style="color: #16a34a; font-size: 24px;">$${futureValue.toLocaleString('en-US', {maximumFractionDigits: 0})}</span>`;
}
</script>

---

*News aggregated from Google News RSS feeds.*
