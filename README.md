# Artificial CU - AI-Enhanced Lending Decision Demo

**A web prototype demonstrating how AI and open banking create fairer lending decisions for credit unions.**

---

## Overview

This interactive demo shows Mississippi credit union CEOs how AI-enhanced underwriting combined with open banking data can identify creditworthy members that traditional systems would decline. The demo tells the story of Marcus Johnson, a gig economy worker with a 620 credit score who is approved for a $5,000 auto loan based on verified cash flow and perfect payment history.

### Key Message
**Traditional systems see a 620 credit score and say "decline." AI systems see verified income, perfect payment history, and strong financial management and say "approve."**

---

## How to Run

### Option 1: Local File
1. Download the `index.html` file
2. Double-click to open in your browser
3. Or open from command line: `open index.html`

### Option 2: Web Server (Recommended for Presentations)
For smoother performance and easier screen recording:

```bash
# Using Python 3
python -m http.server 8000

# Using Python 2
python -m SimpleHTTPServer 8000

# Using Node.js http-server
npx http-server

# Using Ruby
ruby -run -ehttpd . -p8000
```

Then navigate to `http://localhost:8000` in your browser.

### Recommended Browser Settings for Presentation
- **Resolution**: 1920x1080 (matches your presentation size)
- **Zoom**: 100% (default)
- **Browser**: Chrome or Safari (best performance)
- **Full-screen**: Press F11 or Cmd+Ctrl+F

---

## Demo Flow

### Screen 1: Application Form (Immediate)
- Shows member details: Marcus Johnson
- Displays traditional credit score: **620** (prominently in amber warning color)
- User clicks "Analyze Application" button

### Screen 2: Traditional Analysis (2.5 seconds)
- Shows what a traditional credit system sees:
  - Credit score: 620 (below threshold)
  - DTI: Unable to calculate
  - Employment: Pending verification
- **Decision: DECLINE**
- Automatically transitions with "Running AI-enhanced analysis..." message

### Screen 3: AI Analysis Dashboard (Main Demo)
**Timing breakdown:**
- Data sources load sequentially: 0-4 seconds (800ms between each)
- AI reasoning appears: 4.5-7 seconds (5 items with staggered animations)
- Decision panel and comparison box: 7.5+ seconds

**Key elements:**
- **Left panel**: Connected data sources "light up" as they load
  - Primary Account (Artificial CU)
  - Connected Accounts (Open Banking)
  - Income Analysis
  - Payment History
  - Spending Patterns

- **Right panel**: AI reasoning in plain English
  - Income Verification ✓
  - Payment Behavior ✓
  - Cash Flow Management ✓
  - Current Capacity ✓
  - Credit Score Context ⚠️

- **Decision Panel**: Green approval with:
  - Risk: LOW
  - Rate: 6.75% APR
  - Payment: $149.50/36 months
  - Confidence: 94%

- **Comparison Box**: Traditional vs AI-Enhanced
- **Expandable Section**: Detailed explanation of reasoning, privacy controls, and impact

### Interactive Elements
- **"Start Over"** button: Resets to initial form
- **"Compare Systems"** button: Scrolls to comparison box
- **"View Data Sources"** button: Scrolls to data panel
- **"Why this decision?"** expandable: Shows detailed explanation
- **Hover effects**: Data source cards highlight on hover

---

## Customization Guide

### Text Content

All text is easily customizable in the HTML. Search for these fields:

**Member Details (Screen 1)**
```html
<input type="text" value="Marcus Johnson" disabled>
<input type="text" value="$5,000" disabled>
<input type="text" value="Used Auto Purchase" disabled>
<div class="credit-score-value">620</div>
```

**Credit Union Name**
```html
<h1>Artificial CU</h1>
<p>Member-First Lending</p>
```

**Data Values (Screen 3 Left Panel)**
Update all the `<span class="data-value">` values:
```html
<span class="data-value">$340</span>  <!-- Checking balance -->
<span class="data-value">$2,100</span>  <!-- Savings balance -->
<!-- etc. -->
```

**AI Reasoning Text (Screen 3 Right Panel)**
Update the `.reasoning-text` sections:
```html
<div class="reasoning-text">
    Despite non-traditional income sources, Marcus demonstrates
    consistent earnings of $2,400/month across gig platforms...
</div>
```

### Colors

Edit the CSS custom properties at the top of the `<style>` section:

```css
:root {
    --color-primary: #2C5F7C;        /* Main credit union blue */
    --color-success: #27AE60;        /* Approvals, checkmarks */
    --color-warning: #F39C12;        /* Traditional alerts */
    --color-decline: #E74C3C;        /* Decline decision */
    --color-background: #F8F9FA;     /* Light background */
    --color-text-dark: #2C3E50;      /* Main text */
    --color-text-light: #7F8C8D;     /* Secondary text */
    --color-accent: #3498DB;         /* Interactive elements */
    --color-white: #FFFFFF;          /* White */
    --color-border: #E0E6ED;         /* Borders */
}
```

**Example**: To change the primary color to a different blue:
```css
--color-primary: #1A5276;  /* Darker blue */
```

### Timing & Animations

All timing is controlled in the JavaScript section. Find these key timing constants:

**Traditional analysis duration** (currently 2.5 seconds):
```javascript
setTimeout(() => {
    showScreen('ai');
}, 2500);  // Change this value
```

**Data source loading delays** (currently 800ms between each):
```javascript
const sources = [
    { id: 'source-1', delay: 0 },      // First one immediate
    { id: 'source-2', delay: 800 },    // 0.8 seconds after first
    { id: 'source-3', delay: 1600 },   // 1.6 seconds
    { id: 'source-4', delay: 2400 },   // 2.4 seconds
    { id: 'source-5', delay: 3200 }    // 3.2 seconds
];
```

**AI reasoning animation delays** (in CSS):
```css
.reasoning-item:nth-child(1) { animation-delay: 4.5s; }
.reasoning-item:nth-child(2) { animation-delay: 5.1s; }
.reasoning-item:nth-child(3) { animation-delay: 5.7s; }
/* etc. */
```

To speed up the entire demo, reduce all animation delays proportionally.

### Typography

Adjust font sizes in the CSS:

```css
.form-header h2 {
    font-size: 32px;  /* Change form title size */
}

.ai-header h2 {
    font-size: 32px;  /* Change AI dashboard title */
}

.decision-recommendation {
    font-size: 28px;  /* Change "APPROVE" size */
}
```

For presentations, larger fonts are better. Consider increasing these by 10-15% for visibility from 10+ feet away.

### Financial Data

To change Marcus's financial profile, update these sections:

**Income** (Screen 3, left panel):
```html
<span class="data-value">$1,800</span>  <!-- Uber income -->
<span class="data-value">$600</span>    <!-- DoorDash income -->
<span class="data-value">$2,400</span>  <!-- Total -->
```

**Balances**:
```html
<span class="data-value">$340</span>   <!-- Checking -->
<span class="data-value">$2,100</span> <!-- Savings -->
<span class="data-value">$890</span>   <!-- Chase checking -->
```

**Decision Parameters** (Screen 3, decision panel):
```html
<div class="decision-stat-value">LOW</div>        <!-- Risk -->
<div class="decision-stat-value">6.75%</div>     <!-- APR -->
<div class="decision-stat-value">$149.50</div>   <!-- Payment -->
<span class="confidence-value">94%</span>        <!-- Confidence -->
```

---

## Technical Details

### File Structure
```
Demo 01 - Proactive Guardian/
├── index.html           (Main application - single file)
├── README.md           (This file)
└── [Optional] screenshot.png  (For documentation)
```

### Technologies
- **HTML5**: Semantic markup
- **CSS3**: Grid, Flexbox, CSS animations, custom properties
- **Vanilla JavaScript**: No frameworks or dependencies
- **Browser Compatible**: Chrome, Safari, Firefox, Edge

### Performance Optimizations
- Single HTML file = instant loading
- CSS animations run on GPU (smooth 60fps)
- No external dependencies = works offline
- Responsive design adapts to any screen size

### Accessibility Features
- Semantic HTML structure
- ARIA-friendly color contrast
- High visibility for presentation contexts
- Readable font sizes (16px minimum)

### Key JavaScript Functions

```javascript
showScreen(screenName)          // Transition between screens
submitApplication(e)            // Handle form submission
startDataLoadingAnimation()      // Animate data source loading
resetDemo()                      // Reset to initial state
toggleExpanded(header)           // Toggle explanation panel
toggleComparison()               // Scroll to comparison
toggleDetails()                  // Scroll to data sources
```

---

## Presentation Tips

### Screen Recording
1. Open in Chrome at 1920x1080
2. Set browser zoom to 100%
3. Use tools like QuickTime (Mac), OBS (all platforms), or built-in screen recording
4. Move cursor deliberately to show interaction
5. Pause on the decision panel to let it sink in

### Live Demonstration
1. Load in browser before presenting (no network needed)
2. Use "Start Over" button between demonstrations
3. Speak to the comparison box - this is the "aha moment"
4. Expand the "Why this decision?" section to discuss privacy
5. Emphasize the 94% confidence score vs. traditional decline

### Discussion Points
- **"Notice the credit score - 620. Traditional system declines automatically."**
- **"But look at the data - perfect payment history, verified income, positive savings."**
- **"This person is NOT a credit risk. They just don't fit the old model."**
- **"With open banking and AI, you can see members traditional systems can't."**
- **"This is competitive advantage. Fintechs are doing this now."**
- **"Your mission is financial inclusion - this technology makes that possible."**

### Customization for Your Institution
- Change "Artificial CU" to your credit union name
- Update primary colors to match your branding
- Adjust member profile to match your target market
- Modify loan amount and terms to typical products

---

## Troubleshooting

### Demo won't start
- Clear browser cache (Cmd+Shift+R on Mac, Ctrl+Shift+R on Windows)
- Try a different browser
- Disable browser extensions (especially ad blockers)

### Animations are jerky
- Close other applications
- Update your browser to latest version
- Try Chrome or Safari (best animation performance)

### Text appears too small
- Increase font sizes in CSS (see Customization section)
- Or use browser zoom (Cmd+Plus on Mac, Ctrl+Plus on Windows)
- Consider 150% zoom for presentations to large audiences

### Data isn't visible at certain screen sizes
- This is intentional responsive design
- For presentations, lock at 1920x1080
- On mobile/tablet, panels stack vertically

---

## Data Source

All data is hardcoded for the demo:
- **No API calls needed**
- **No database required**
- **Works completely offline**
- **All numbers are realistic based on actual gig economy worker profiles**

The financial profile reflects:
- Average gig economy income in Mississippi
- Typical savings and spending patterns
- Real-world payment behavior of responsible borrowers
- Authentic credit score impact of thin credit files

---

## Browser Compatibility

| Browser | Version | Status |
|---------|---------|--------|
| Chrome | Latest | ✅ Full support |
| Safari | Latest | ✅ Full support |
| Firefox | Latest | ✅ Full support |
| Edge | Latest | ✅ Full support |
| Internet Explorer | Any | ❌ Not supported |

---

## File Size & Loading

- **HTML file size**: ~75 KB (single file, all CSS and JS included)
- **Load time**: <100ms locally
- **Network bandwidth**: Zero (all hardcoded)
- **Storage**: Minimal - single file

---

## Support & Customization

### For Quick Changes
1. Open `index.html` in your favorite text editor
2. Use Ctrl+F or Cmd+F to find the text you want to change
3. Save the file
4. Refresh your browser (Cmd+R or Ctrl+R)

### For Advanced Customization
- All CSS is organized with clear comments
- All JavaScript functions are documented
- Color palette uses CSS custom properties (easy to change globally)
- Timing values are in milliseconds (easy to adjust)

---

## Version History

**Version 1.0** (October 29, 2024)
- Initial release
- Complete demo flow: Application → Traditional Analysis → AI Analysis
- Animated data loading and AI reasoning
- Comparison framework
- Expandable explanation section
- Fully responsive design
- Customizable timing, colors, and content

---

## Legal & Disclaimers

This is a **demonstration prototype** not an actual lending platform. It shows:
- ✅ How the user interface could work
- ✅ How decision logic could be presented
- ✅ How to communicate AI reasoning in plain language
- ✅ Privacy and compliance considerations

This does **not**:
- ❌ Actually process loan applications
- ❌ Make binding lending decisions
- ❌ Connect to real financial data
- ❌ Comply with all banking regulations without additional work

For production use:
- Integrate with real open banking APIs (Plaid, FDX, Finicity)
- Implement actual AI/ML models
- Add proper authentication and data security
- Ensure GLBA, FCRA, and state lending law compliance
- Include human credit officer review process
- Add proper audit logging

---

## Questions?

Review the key sections above:
- **"How to Run"** for setup
- **"Customization Guide"** for changes
- **"Presentation Tips"** for using the demo effectively
- **"Technical Details"** for the architecture

Edit boldly - this is designed to be customized for your needs.

Good luck with your keynote! 🚀
