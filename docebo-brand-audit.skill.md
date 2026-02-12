---
name: docebo-brand-audit
description: Analyze any web page, dashboard, or artifact against Docebo brand guidelines. Use this skill to audit brand compliance, identify discrepancies, and get specific recommendations for improvements. Invoke when reviewing Docebo-branded content, checking design consistency, or preparing materials for brand review.
---

# Docebo Brand Audit Skill

This skill audits web pages, dashboards, and digital artifacts against Docebo's official brand system. It identifies compliance issues, suggests improvements, and provides specific code fixes.

## How to Use

When invoked, this skill will:
1. Analyze the target content (URL, HTML file, or code)
2. Check against all brand guidelines
3. Produce a structured audit report with severity ratings
4. Provide specific, actionable fixes

## Audit Checklist

### 1. Color Compliance

#### Primary Colors (Required)
| Color | Hex | Check For |
|-------|-----|-----------|
| Docebo Blue | `#0057FF` | Primary brand color - headers, CTAs, hero backgrounds |
| Black | `#2A2923` | Text on light backgrounds (NOT pure #000000) |
| White | `#FFFFFF` | Text on dark/colored backgrounds |
| Dark | `#131E29` | Navigation, footer, dark sections |

#### Secondary Colors
| Color | Hex | Check For |
|-------|-----|-----------|
| Light Blue | `#4C8DFF` | Secondary buttons, hover states |
| Navy | `#0033A0` | Gradients with Docebo Blue, alternate dark sections |

#### Accent Colors (Should be used sparingly)
| Color | Hex | Correct Usage | Common Mistake |
|-------|-----|---------------|----------------|
| Pink Neon | `#FF5DD8` | Small highlights, badges | Using as hero background |
| Green | `#54FA77` | Success states, positive metrics | Overuse in non-metric contexts |
| Purple Neon | `#7E2EE9` | Feature callouts, small accents | Using as primary section color |
| Yellow-Green | `#E3FFAB` | Soft highlights, eyebrow labels | Using for body text |

#### Red Flags
- [ ] Pure black (#000000) used instead of Docebo Black (#2A2923)
- [ ] Random hex values not in Phoenix palette
- [ ] Accent colors used for large areas (heroes, full sections)
- [ ] Low contrast text (fails WCAG AA)
- [ ] Gradients not using approved combinations (blue→navy, navy→blue)

### 2. Typography Compliance

#### Required Fonts
```css
--font-heading: 'Space Grotesk', sans-serif;  /* Headlines, titles, large numbers */
--font-body: 'Inter', sans-serif;              /* Body text, labels, descriptions */
```

#### Size Hierarchy (Web/Dashboards)
| Element | Expected Size | Weight |
|---------|---------------|--------|
| Hero/Page title | 48px (clamp 32-48px) | 700 |
| Section heading (H2) | 24px | 700 |
| Card title | 18px | 600-700 |
| KPI number | 36-48px | 700 |
| KPI label | 12px uppercase | 500 |
| Body text | 14-16px | 400 |
| Eyebrow label | 12px uppercase, 0.1em spacing | 500 |

#### Red Flags
- [ ] System fonts (Arial, Helvetica) used instead of Space Grotesk/Inter
- [ ] Heading font used for body text
- [ ] Missing Google Fonts import
- [ ] Inconsistent size hierarchy
- [ ] Missing letter-spacing on eyebrow labels

### 3. Voice & Tone Compliance

#### Banned Words (AI-Speak)
These words indicate unedited AI content and must be removed:
- "delve", "realm", "ever-evolving", "navigate", "embark"
- "tapestry", "landscape" (as metaphor), "leverage" (as verb)
- "utilize", "synergy", "robust", "seamless" (when generic)
- "game-changing", "cutting-edge"

#### Banned Patterns
- [ ] Em dashes (—) - use semicolons instead
- [ ] "In today's rapidly..." openings
- [ ] "...and beyond" endings
- [ ] "In conclusion," "To summarize," transitions
- [ ] Title Case Headlines (should be Sentence case)
- [ ] ALL CAPS (except eyebrow labels and acronyms)

#### Required Patterns
- [x] Oxford comma ("learn, grow, and succeed")
- [x] Contractions ("Let's build" not "Let us build")
- [x] American English ("customize" not "customise")
- [x] Active voice ("We built" not "It was built")
- [x] Outcome-focused language

### 4. Layout & Component Compliance

#### Hero Sections
```css
/* Correct hero pattern */
.hero {
  background: linear-gradient(135deg, var(--docebo-blue) 0%, var(--docebo-navy) 100%);
  /* OR solid: background: var(--docebo-blue); */
  color: white;
  padding: 60-80px 40-48px;
}
```

#### Cards
```css
/* Correct card pattern */
.card {
  background: var(--docebo-white);
  border: 1px solid var(--neutral-200); /* #E1DBD2 */
  border-radius: 10px; /* var(--radius-md) */
  padding: 24px;
}
```

#### KPI/Stat Cards
- Large number (Space Grotesk, 36-48px, 700 weight)
- Small label above or below (uppercase, 12px, letter-spacing)
- Optional change indicator (green for positive, pink for negative)

#### Navigation
- Dark background (#131E29)
- White text
- Active tab: Docebo Blue background
- Sticky positioning recommended

### 5. Asset Usage Guidelines

#### When to Use Logo
| Context | Logo Version |
|---------|--------------|
| Light backgrounds | Blue logo or Black logo |
| Dark/Blue backgrounds | White logo |
| Favicons | 60x60 or 110x110 square versions |

#### When to Use Photography
1. **First choice**: Authentic Docebo customer/event photos
2. **Second choice**: Authentic team photos
3. **Last resort**: Candid stock photos (avoid corporate clichés)

#### When to Use Icons
- Consistent style throughout (outline OR filled, not mixed)
- Accent color for icon backgrounds, not the icons themselves
- Size: 24-32px for inline, 48-64px for feature cards

### 6. Accessibility Checks

#### Contrast Requirements (WCAG AA)
| Combination | Passes? | Use For |
|-------------|---------|---------|
| White on Docebo Blue (#0057FF) | Large text only | Headers, buttons |
| White on Dark (#131E29) | AAA | Body text on dark |
| Black (#2A2923) on White | AAA | Primary body text |
| Docebo Blue on White | Large text only | Links, headers |

#### Required Accessibility Features
- [ ] Alt text on all images
- [ ] Focus states on interactive elements
- [ ] No color-only information encoding
- [ ] Sufficient font sizes (min 14px body)

---

## Audit Report Template

When performing an audit, structure the output as follows:

```markdown
# Brand Audit Report: [Page/Asset Name]

## Summary
- **Overall Compliance**: [High/Medium/Low]
- **Critical Issues**: [count]
- **Warnings**: [count]
- **Suggestions**: [count]

## Critical Issues (Must Fix)
### Issue 1: [Title]
- **Location**: [file:line or CSS selector]
- **Current**: [what's wrong]
- **Expected**: [what it should be]
- **Fix**:
```[code fix]```

## Warnings (Should Fix)
...

## Suggestions (Nice to Have)
...

## What's Working Well
- [Positive finding 1]
- [Positive finding 2]
```

---

## Quick Reference: CSS Custom Properties

Copy this block to ensure brand compliance:

```css
:root {
  /* Primary */
  --docebo-blue: #0057FF;
  --docebo-black: #2A2923;
  --docebo-white: #FFFFFF;
  --docebo-dark: #131E29;

  /* Secondary */
  --docebo-light-blue: #4C8DFF;
  --docebo-navy: #0033A0;

  /* Accents (use sparingly) */
  --docebo-pink: #FF5DD8;
  --docebo-green: #54FA77;
  --docebo-purple: #7E2EE9;
  --docebo-yellow-green: #E3FFAB;
  --docebo-light-purple: #DCB7FF;
  --docebo-beige: #E6DACB;

  /* Neutrals */
  --neutral-50: #F6F5F2;
  --neutral-100: #EBE6DD;
  --neutral-200: #E1DBD2;
  --neutral-400: #807B74;
  --neutral-600: #56534E;
  --neutral-900: #2A2923;

  /* Typography */
  --font-heading: 'Space Grotesk', sans-serif;
  --font-body: 'Inter', sans-serif;

  /* Spacing */
  --radius-sm: 6px;
  --radius-md: 10px;
  --radius-lg: 16px;
}
```

---

## Common Fixes

### Fix: Wrong text color
```css
/* Wrong */
color: #000000;
color: black;

/* Correct */
color: var(--docebo-black); /* #2A2923 */
```

### Fix: Non-brand gradient
```css
/* Wrong */
background: linear-gradient(135deg, #0057FF, #7E2EE9);

/* Correct */
background: linear-gradient(135deg, var(--docebo-blue) 0%, var(--docebo-navy) 100%);
```

### Fix: Missing font import
```html
<!-- Add to <head> -->
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;500;700&family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
```

### Fix: Title Case heading
```html
<!-- Wrong -->
<h1>Welcome To The Dashboard</h1>

<!-- Correct -->
<h1>Welcome to the dashboard</h1>
```

### Fix: Em dash usage
```markdown
<!-- Wrong -->
The platform — built for enterprise — delivers results.

<!-- Correct -->
The platform; built for enterprise; delivers results.
```
