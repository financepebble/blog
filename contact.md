---
layout: page
title: Contact Us
permalink: /contact/
---

<link rel="stylesheet" href="{{ '/assets/css/custom.css' | relative_url }}">
<div class="contact-container">
<div class="cta-box" style="margin-left: 0; width: 100%;">
  <h3>Get in Touch</h3>
  <p>Whether you have a specific question, a story to share about your journey, or just want to say hello—I’m listening.</p>
  <p><em>Note: While I can share my research and experience, please consult a  professional CPA, CFP or Attorney for your specific  needs.</em></p>
</div>

<script async data-uid="5e6455d259" src="https://financepebble.kit.com/5e6455d259/index.js"></script>
</div>
<style>
  /* 1. Layout & Glassmorphism Styling */
  .contact-container {
    margin-top: 30px;
  }

  .cta-box {
    /* Offset to the right as requested */
    margin-left: 5%;
    width: 95%;
    
    background-color: rgba(128, 128, 128, 0.08);
    backdrop-filter: blur(4px);
    -webkit-backdrop-filter: blur(4px);
    border: 1px solid rgba(128, 128, 128, 0.3);
    border-left: 8px solid #64748b; /* Professional Slate Grey */
    
    padding: 25px;
    margin-bottom: 25px;
    border-radius: 12px;
    color: inherit;
  }

  .cta-box h3 {
    margin-top: 0;
    color: inherit;
  }

  /* 2. Kit Form "Message Box" Hack */
  /* This turns the single-line custom field into a tall text box */
  input[name="fields[message]"] {
    height: 150px !important;
    padding-top: 12px !important;
    vertical-align: top !important;
    line-height: 1.5 !important;
  }

  /* 3. Mobile Responsiveness */
  @media (max-width: 600px) {
    .cta-box {
      margin-left: 0;
      width: 100%;
    }
  }

 /* --- MILLS TEMPLATE FIXES --- */

/* 1. Remove the white box background and borders */
.ck_form.ck_minimal, 
.ck_form.ck_minimal .ck_form_fields {
  background: transparent !important;
  border: none !important;
  box-shadow: none !important;
}

/* 2. Force all text (Headers, Labels, Inputs) to inherit your theme colors */
.ck_form.ck_minimal h3,
.ck_form.ck_minimal .ck_help_block,
.ck_form.ck_minimal label,
.ck_form.ck_minimal .ck_input {
  color: inherit !important;
}

/* 3. Make the input boxes (Email & Message) look good in both modes */
.ck_form.ck_minimal .ck_input {
  background-color: rgba(128, 128, 128, 0.1) !important;
  border: 1px solid rgba(128, 128, 128, 0.3) !important;
  border-radius: 4px !important;
}

/* 4. Ensure the Button doesn't disappear */
.ck_form.ck_minimal .ck_subscribe_button {
  background-color: #475569 !important; /* Slate Blue-Grey */
  color: #ffffff !important;
  text-shadow: none !important;
}

/* 5. The "Success Message" fix */
.ck_form.ck_minimal .ck_success {
  color: inherit !important;
  background: transparent !important;
  border: 1px solid #64748b !important;
}
/* --- ULTIMATE KIT TRANSPARENCY FIX --- */

/* Targets the specific ID and all potential wrapper divs */
[id^="ck_"], 
.ck_form, 
.ck_form_fields, 
.ck_form_container,
.ck_minimal {
  background-color: transparent !important;
  background: transparent !important;
  border: none !important;
  box-shadow: none !important;
}

/* Forces the "Message" input and Email input to behave */
.ck_input, 
input[type="text"], 
input[type="email"] {
  background-color: rgba(128, 128, 128, 0.1) !important;
  color: inherit !important;
  border: 1px solid rgba(128, 128, 128, 0.3) !important;
}

/* This targets the text that Kit injects */
.ck_form h3, 
.ck_form p, 
.ck_form label, 
.ck_help_block {
  color: inherit !important;
} 
</style>



## What We Can Help With

- Suggestions for topics
- Error corrections
- Partnership inquiries
- Media requests

## What We Can't Do

We provide general education only—not personalized financial, tax, or legal advice. Consult a CFP, CPA, or attorney for personalized guidance.
