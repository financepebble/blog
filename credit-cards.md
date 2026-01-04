---
layout: page
title: Credit Card Rewards & Sign-Up Bonuses
permalink: /credit-cards/
---

<link rel="stylesheet" href="{{ '/assets/css/custom.css' | relative_url }}">

# Credit Card Rewards & Optimization

Maximize your credit card rewards, find the best sign-up bonuses, and learn strategies to make your spending work for you.

## Credit Card Topics

<div class="portal-grid">
  <div class="portal-card">
    <div class="portal-icon">🎁</div>
    <h3>Sign-Up Bonuses</h3>
    <p>Current best offers, minimum spend strategies, and timing multiple applications for maximum value.</p>
  </div>

  <div class="portal-card">
    <div class="portal-icon">✈️</div>
    <h3>Travel Rewards</h3>
    <p>Airline miles, hotel points, transfer partners, and how to redeem for maximum value on travel.</p>
  </div>

  <div class="portal-card">
    <div class="portal-icon">💵</div>
    <h3>Cash Back Cards</h3>
    <p>Best cash back rates by category, rotating categories, and stacking strategies for extra rewards.</p>
  </div>

  <div class="portal-card">
    <div class="portal-icon">📊</div>
    <h3>Credit Score Impact</h3>
    <p>How applications affect your score, when to apply, and maintaining excellent credit while churning.</p>
  </div>

  <div class="portal-card">
    <div class="portal-icon">🛡️</div>
    <h3>Card Benefits</h3>
    <p>Purchase protection, extended warranties, travel insurance, and other perks you might not know about.</p>
  </div>

  <div class="portal-card">
    <div class="portal-icon">📱</div>
    <h3>Digital Wallets</h3>
    <p>Apple Pay, Google Pay bonuses, and mobile payment rewards optimization strategies.</p>
  </div>
</div>

## This Month's Top Sign-Up Bonuses

<div style="background: #eff6ff; border: 2px solid #1e40af; border-radius: 12px; padding: 2rem; margin: 2rem 0;">
  <h3 style="margin-top: 0; color: #1e40af; font-family: 'Montserrat', sans-serif;">🔥 Featured Offers - January 2026</h3>
  
  <div style="background: white; padding: 1.5rem; border-radius: 8px; margin-bottom: 1rem;">
    <h4 style="margin: 0 0 0.5rem 0; color: #2d3e50;">Chase Sapphire Preferred®</h4>
    <p style="margin: 0 0 0.5rem 0; color: #64748b;">Earn 60,000 bonus points after spending $4,000 in first 3 months</p>
    <p style="margin: 0; font-size: 0.9rem;"><strong>Value:</strong> ~$750 in travel • <strong>Annual Fee:</strong> $95</p>
  </div>

  <div style="background: white; padding: 1.5rem; border-radius: 8px; margin-bottom: 1rem;">
    <h4 style="margin: 0 0 0.5rem 0; color: #2d3e50;">American Express Gold Card</h4>
    <p style="margin: 0 0 0.5rem 0; color: #64748b;">Earn 60,000 Membership Rewards points after $4,000 spend</p>
    <p style="margin: 0; font-size: 0.9rem;"><strong>Value:</strong> ~$600 in travel • <strong>Annual Fee:</strong> $250</p>
  </div>

  <div style="background: white; padding: 1.5rem; border-radius: 8px;">
    <h4 style="margin: 0 0 0.5rem 0; color: #2d3e50;">Citi Double Cash Card</h4>
    <p style="margin: 0 0 0.5rem 0; color: #64748b;">2% cash back on all purchases (1% when you buy, 1% when you pay)</p>
    <p style="margin: 0; font-size: 0.9rem;"><strong>Value:</strong> Ongoing rewards • <strong>Annual Fee:</strong> $0</p>
  </div>

  <p style="margin-top: 1.5rem; font-size: 0.85rem; color: #64748b;"><em>Offers change frequently. Always check official card issuer websites for current terms.</em></p>
</div>

## Rewards Strategy Tips

<div class="info-box">
  <h3 style="margin-top: 0; color: #1e40af;">💡 Pro Tips for Maximizing Rewards</h3>
  <ul style="margin: 0; padding-left: 1.5rem;">
    <li style="margin-bottom: 0.5rem;"><strong>Pay in full monthly:</strong> Interest charges negate any rewards</li>
    <li style="margin-bottom: 0.5rem;"><strong>Track category bonuses:</strong> Use the right card for each purchase</li>
    <li style="margin-bottom: 0.5rem;"><strong>Time sign-ups strategically:</strong> Apply when you have large planned expenses</li>
    <li style="margin-bottom: 0.5rem;"><strong>Don't overspend for rewards:</strong> Only worth it if you'd buy anyway</li>
    <li><strong>Set reminders for annual fees:</strong> Evaluate if cards are still worth keeping</li>
  </ul>
</div>

## Recent Credit Card Posts

<ul class="post-list">
  {% for post in site.categories.credit-cards limit:10 %}
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
      <p style="color: #64748b;">Posts coming soon! Check back for the latest credit card offers and strategies.</p>
    </li>
  {% endfor %}
</ul>
