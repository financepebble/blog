---
layout: page
title: Financial News
permalink: /market-news/
---

# Financial News & Market Data

Stay updated with the latest in retirement planning, personal finance, and tax strategies.

---

## Live Financial News

<iframe src="https://news.google.com/rss/search?q=retirement+planning+401k+personal+finance&hl=en-US&gl=US&ceid=US:en" 
        style="display:none;" 
        onload="loadGoogleNews(this, 'retirement-news')"></iframe>
<div id="retirement-news" style="margin: 2rem 0;">
  <h3 style="font-family: 'Playfair Display', serif; color: #1a1a1a; margin-bottom: 1.5rem;">Latest Retirement & Finance News</h3>
  <p>Loading news...</p>
</div>

<script>
async function loadGoogleNews(iframe, targetId) {
  const url = iframe.src;
  try {
    const response = await fetch(`https://api.rss2json.com/v1/api.json?rss_url=${encodeURIComponent(url)}`);
    const data = await response.json();
    
    if (data.items && data.items.length > 0) {
      let html = '<div style="display: grid; grid-template-columns: repeat(auto-fill, minmax(350px, 1fr)); gap: 1.5rem;">';
      
      data.items.slice(0, 12).forEach(item => {
        const description = item.description ? item.description.replace(/<[^>]*>/g, '').substring(0, 150) : '';
        html += `
          <div style="background: white; border-radius: 16px; padding: 2rem; box-shadow: 0 2px 12px rgba(0,0,0,0.06); transition: all 0.3s;" 
               onmouseover="this.style.transform='translateY(-4px)'; this.style.boxShadow='0 8px 24px rgba(0,0,0,0.12)'" 
               onmouseout="this.style.transform='translateY(0)'; this.style.boxShadow='0 2px 12px rgba(0,0,0,0.06)'">
            <h4 style="margin: 0 0 0.75rem 0; font-family: 'Playfair Display', serif; font-size: 1.3rem; line-height: 1.4;">
              <a href="${item.link}" target="_blank" style="color: #1a1a1a; text-decoration: none;">
                ${item.title}
              </a>
            </h4>
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

<div class="info-box" style="max-width: 600px;">
  <h3 style="margin-top: 0; color: #1e40af;">Quick Retirement Savings Goal</h3>
  
  <div style="margin-bottom: 1rem;">
    <label style="display: block; margin-bottom: 0.5rem; font-weight: 500;">Current Age:</label>
    <input type="number" id="age" value="30" style="width: 100%; padding: 1rem; border: 2px solid #e5e7eb; border-radius: 12px; font-family: 'Inter', sans-serif;">
  </div>
  
  <div style="margin-bottom: 1rem;">
    <label style="display: block; margin-bottom: 0.5rem; font-weight: 500;">Retirement Age:</label>
    <input type="number" id="retireAge" value="65" style="width: 100%; padding: 1rem; border: 2px solid #e5e7eb; border-radius: 12px; font-family: 'Inter', sans-serif;">
  </div>
  
  <div style="margin-bottom: 1rem;">
    <label style="display: block; margin-bottom: 0.5rem; font-weight: 500;">Current Savings ($):</label>
    <input type="number" id="savings" value="50000" style="width: 100%; padding: 1rem; border: 2px solid #e5e7eb; border-radius: 12px; font-family: 'Inter', sans-serif;">
  </div>
  
  <div style="margin-bottom: 1rem;">
    <label style="display: block; margin-bottom: 0.5rem; font-weight: 500;">Monthly Contribution ($):</label>
    <input type="number" id="monthly" value="500" style="width: 100%; padding: 1rem; border: 2px solid #e5e7eb; border-radius: 12px; font-family: 'Inter', sans-serif;">
  </div>
  
  <div style="margin-bottom: 1.5rem;">
    <label style="display: block; margin-bottom: 0.5rem; font-weight: 500;">Expected Annual Return (%):</label>
    <input type="number" id="return" value="7" style="width: 100%; padding: 1rem; border: 2px solid #e5e7eb; border-radius: 12px; font-family: 'Inter', sans-serif;">
  </div>
  
  <button onclick="calculate()" class="btn" style="width: 100%;">Calculate My Timeline</button>
  
  <div id="result" style="margin-top: 1.5rem;"></div>
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
    `<div style="background: white; padding: 1.5rem; border-radius: 12px; margin-top: 1rem; box-shadow: 0 2px 8px rgba(0,0,0,0.05);">
      <p style="margin: 0 0 0.5rem 0; color: #666;">At age <strong>${retireAge}</strong>, you'll have:</p>
      <p style="margin: 0; font-size: 2rem; color: #16a34a; font-weight: 700; font-family: 'Playfair Display', serif;">
        $${futureValue.toLocaleString('en-US', {maximumFractionDigits: 0})}
      </p>
    </div>`;
}
</script>

---

<p style="text-align: center; color: #999; font-size: 0.9rem; margin-top: 3rem;">
  News aggregated from Google News RSS feeds • Calculator uses standard compound interest formula
</p>
