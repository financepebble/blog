---
layout: page
title: Early Retirement Planning
permalink: /retirement/
---

<link rel="stylesheet" href="{{ '/assets/css/custom.css' | relative_url }}">

# Early Retirement & FIRE

Achieve financial independence and retire early with proven strategies. Whether you're aiming for traditional retirement at 65 or aggressive FIRE by 45, we'll help you create a roadmap.

## Key Topics

<div class="portal-grid">
  <div class="portal-card">
    <div class="portal-icon">🎯</div>
    <h3>FIRE Movement</h3>
    <p>Financial Independence, Retire Early explained. Learn about Lean FIRE, Fat FIRE, and Barista FIRE approaches.</p>
  </div>

  <div class="portal-card">
    <div class="portal-icon">💼</div>
    <h3>401(k) Strategies</h3>
    <p>Maximize employer match, understand vesting, and optimize contribution levels for your situation.</p>
  </div>

  <div class="portal-card">
    <div class="portal-icon">🏦</div>
    <h3>IRA Options</h3>
    <p>Traditional vs. Roth IRA, backdoor Roth conversions, and contribution limit strategies.</p>
  </div>

  <div class="portal-card">
    <div class="portal-icon">🧮</div>
    <h3>FIRE Calculator</h3>
    <p>Calculate your FI number, determine your savings rate, and project your retirement timeline.</p>
  </div>

  <div class="portal-card">
    <div class="portal-icon">📊</div>
    <h3>Asset Allocation</h3>
    <p>Portfolio strategies for different life stages. Balance growth and preservation as you approach FI.</p>
  </div>

  <div class="portal-card">
    <div class="portal-icon">💡</div>
    <h3>Withdrawal Strategies</h3>
    <p>The 4% rule, variable withdrawal rates, and tax-efficient drawdown strategies.</p>
  </div>
</div>

## Retirement Calculator

<div style="background: #f8f9fa; padding: 2rem; border-radius: 12px; margin: 2rem 0; max-width: 600px;">
  <h3 style="margin-top: 0; font-family: 'Montserrat', sans-serif;">Quick FIRE Number Calculator</h3>
  
  <label style="display: block; margin-bottom: 0.5rem; font-weight: 500;">Annual Expenses: $</label>
  <input type="number" id="expenses" value="50000" style="width: 100%; padding: 0.75rem; margin-bottom: 1rem; border: 1px solid #e2e8f0; border-radius: 8px;">
  
  <label style="display: block; margin-bottom: 0.5rem; font-weight: 500;">Current Savings: $</label>
  <input type="number" id="savings" value="100000" style="width: 100%; padding: 0.75rem; margin-bottom: 1rem; border: 1px solid #e2e8f0; border-radius: 8px;">
  
  <label style="display: block; margin-bottom: 0.5rem; font-weight: 500;">Monthly Savings: $</label>
  <input type="number" id="monthly" value="2000" style="width: 100%; padding: 0.75rem; margin-bottom: 1rem; border: 1px solid #e2e8f0; border-radius: 8px;">
  
  <button onclick="calculateFIRE()" style="width: 100%; padding: 1rem; background: #1e40af; color: white; border: none; border-radius: 8px; font-weight: 600; cursor: pointer; margin-top: 1rem;">Calculate My FIRE Timeline</button>
  
  <div id="fireResult" style="margin-top: 1.5rem; font-size: 1.1rem;"></div>
</div>

<script>
function calculateFIRE() {
  const expenses = parseFloat(document.getElementById('expenses').value);
  const savings = parseFloat(document.getElementById('savings').value);
  const monthly = parseFloat(document.getElementById('monthly').value);
  
  // FIRE number using 4% rule (25x annual expenses)
  const fireNumber = expenses * 25;
  const needToSave = fireNumber - savings;
  const monthsToFIRE = needToSave / monthly;
  const yearsToFIRE = (monthsToFIRE / 12).toFixed(1);
  
  document.getElementById('fireResult').innerHTML = `
    <div style="background: white; padding: 1.5rem; border-radius: 8px; border: 2px solid #1e40af;">
      <p style="margin: 0 0 1rem 0;"><strong>Your FIRE Number:</strong> $${fireNumber.toLocaleString()}</p>
      <p style="margin: 0 0 1rem 0;"><strong>Still Need to Save:</strong> $${needToSave.toLocaleString()}</p>
      <p style="margin: 0; font-size: 1.3rem; color: #1e40af;"><strong>Years Until FIRE:</strong> ${yearsToFIRE} years</p>
    </div>
    <p style="margin-top: 1rem; font-size: 0.9rem; color: #64748b;">Based on the 4% safe withdrawal rule. Assumes 7% average annual returns.</p>
  `;
}
</script>

## Recent Retirement Posts

<ul class="post-list">
  {% for post in site.categories.retirement limit:10 %}
    <li>
      <span class="post-meta">{{ post.date | date: "%b %-d, %Y" }}</span>
      <h3>
        <a class="post-link" href="{{ post.url | relative_url }}">
          {{ post.title | escape }}
        </a>
      </h3>
    </li>
  {% else %}
    <li>
      <p style="color: #64748b;">Posts coming soon! Check back regularly for retirement planning strategies.</p>
    </li>
  {% endfor %}
</ul>

---

<div class="info-box">
  <strong>💡 Getting Started:</strong> Most experts recommend saving 15-20% of your income for traditional retirement, or 50%+ for aggressive FIRE. Use our calculator above to see your personalized timeline.
</div>
