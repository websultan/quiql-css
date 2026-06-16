# 📜 Quiql CSS v1.0 — The "Golden Mean" CSS Methodology

**Quiql CSS** is an ultra-efficient architectural methodology designed specifically for classic multi-page web development (HTML, PHP, Blade, Pug, CMS). It preserves the strict encapsulation of BEM while adopting the brevity of Tailwind, radically reducing HTML payload size without losing semantics.

---

## 🎯 Why Quiql? (Problem — Solution)

*   **The BEM Problem:** Bloated, over-engineered HTML code with endless class names (`product-card__button--disabled-primary`). It increases network payload and harms scannability.
*   **The Tailwind Problem:** Chaotic utility-first soup in HTML, complete destruction of semantics, and maintenance hell when dealing with server-side CMS templates.
*   **The Quiql Solution:** HTML stays lightweight and semantic. Styles are completely isolated using short, recognizable module aliases (`pCd_`), while selector specificity in CSS is kept flat with a baseline of `0,1,0` and strictly controlled growth.

---

## 🌳 Green IT & Eco-Efficiency (Win-Win-Win-Win)
**A quadruplicate victory: Better for Businesses, Users, Developers, and the Planet.**

Quiql is an integral part of the **Sustainable Web Development** movement. By drastically shortening class names and completely eliminating deep nesting, Quiql reduces structural code weight by up to **2.5 times** compared to Tailwind.

At **1,000,000 page views per day** (assuming a baseline 200KB page weight on Tailwind), switching to Quiql CSS saves:
*   **41.7 Terabytes of network traffic per year.**
*   **6,683 kWh of electricity** (enough to fully power an average apartment for over 2.5 years).
*   **2,954 kg of $CO_2$ emissions per year** (equivalent to the amount absorbed by 135 mature trees growing for an entire year).

---

### 💬 The "But We Have Gzip/Brotli" Counter-Argument

Some developers argue that HTML bloat doesn't matter because text compression algorithms (Gzip or Brotli) shrink repeated Tailwind classes anyway. However, this ignores a critical engineering reality: **compression and decompression are NOT computationally free.**

*   **Server-Side CPU Tax:** At **1,000,000 daily views**, dynamically compressing heavily bloated HTML strings on the fly creates an ongoing computing bottleneck for backend servers, spiking CPU utilization and data-center power consumption.
*   **Client-Side Battery Drain:** Decompression and DOM parsing happen entirely on the user's device. Millions of smartphones—especially low-end mobile devices—continuously burn their battery charge and CPU cycles just to unpack, read, and expand chaotic, endless inline utility strings in browser memory.
*   **The Quiql Advantage:** By keeping the raw HTML lightweight and semantic from the very beginning, Quiql radically minimizes the overall energy and hardware footprint of both **server-side runtime compression** and **client-side parsing**.

---

## 📊 Syntax Cheatsheet (Unique Architecture Tokens)

Thanks to its strict token system, Quiql is 100% predictable for developers and effortlessly validated by automated linters.

| Entity | Architectural Token | Class Example | Purpose |
| :--- | :--- | :--- | :--- |
| **Beacon** | `PascalCase_` (HTML only) | `ProductCard_` | Global `Ctrl+F` navigation locator |
| **Alias** | `camelCase_` (2–4 consonants)| `pCd_` | Local module namespace isolation |
| **Element** | `alias_elementName` | `pCd_title` | Flat component structure element |
| **Atom** | `word-` (trailing hyphen) | `btn-`, `grid-` | Global system-wide layout constructors |
| **Modifier**| `-[name]` (leading hyphen) | `-promo`, `-active`| Role-based style presets |
| **State** | `_[root]` (leading underscore) | `_act`, `_open` | Dynamic state flags toggled via JS |
| **Suffix** | `_[breakpoint]` (trailing) | `-hid_sm`, `_act_md-`| Structural responsive behavior only |

---

## 📜 The Quiql CSS Manifest (11 Core Rules)

### 1. Block Declaration (The Beacon)
Written in `PascalCase_` strictly at the root of the component in HTML. Used solely for global project search (`Ctrl+F`). **Never targeted in CSS.**

### 2. Module Alias (The Alias)
The working name of the block in CSS. Shortened to 2–4 consonants (`uCd_`, `mHdr_`). In case of a namespace collision, the older component retains priority. The newcomer must append a vowel or a digit to resolve it (e.g., `sBr_` → `sbAr_` or `sBr2_`).

### 3. Element Naming & The Official Quiql Vocabulary
Element selectors in CSS are always flat, ignoring HTML hierarchy. To maintain high code density and prevent your HTML from turning into a riddle, Quiql uses a strict, unified 35-token vocabulary for elements, presets, states, and responsive actions. 

Using these exact tokens is **strongly recommended**. If a specific word is not in the vocabulary, or if your team prefers maximum clarity for a unique custom module, you must write the word in full (e.g., `pCd_title` or `-blackFriday`). Custom, unverified, or cryptic abbreviations are strictly prohibited.

#### 📋 The Official Quiql Vocabulary (Unified 35-Token Matrix)

| Category | Full Word | Quiql Token | Category | Full Word | Quiql Token |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Structure** | Button | `btn` | **Style** | Primary | `prm` |
| (Elements & | Image | `img` | (Modifiers & | Secondary | `sec` |
| Atoms) | Title / Heading | `ttl` | Presets) | Success | `suc` |
| | Description | `dsc` | | Danger (Error) | `dng` |
| | Wrapper / Cont. | `wrp` | | Warning | `wrn` |
| | Content | `cnt` | | Info | `inf` |
| | Text | `txt` | | Promo | `prm` |
| | Background | `bg` | | Accent | `acc` |
| | Link | `lnk` | | Inverse | `inv` |
| | Item | `itm` | | Dark | `drk` |
| | List | `lst` | **Responsive**| Small (Mobile) | `sm` |
| | Header | `hdr` | (Breakpoints) | Medium (Tablet) | `md` |
| | Footer | `ftr` | | Large (Desktop)| `lg` |
| **Logic** | Active | `act` | | Extra Large | `xl` |
| (JS States) | Open / Opened | `open` | **Behavior** | Hide | `hid` |
| | Loading | `load` | (Suffix | Visible (Show) | `vis` |
| | Error | `err` | Actions) | Full-width | `full` |
| | | | | Reverse | `rev` |

*   **Anti-Cascade Variable Passing:** If a child element needs to change non-inheritable properties (e.g., `padding`) based on the parent's state, **cascading selectors are forbidden**. Use local CSS variables prefixed with the alias name instead: `--pCd-el-pad`.

### 4. Global Atoms (Global Atoms)
System-level layout and UI primitives (`btn-`, `inp-`). The Atom provides the global base; the local element handles component-specific overrides (`class="btn- pCd_btn"`).

### 5. Modifiers & Presets (Modifiers)
Use encapsulated role presets (`-promo`) instead of utility-first class bloating (`-red -bold -szLg`).
*   **Chaining (No Cascade):** To resolve modifier intersections, chain selectors without spaces. In CSS, they **must be written in alphabetical order**: `.pCd_btn.-active.-red`.
*   **Pseudo-classes:** Native pseudo-classes must always be placed at the very end of the selector chain: `.pCd_btn.-active.-red:hover`. Using element classes inside functional pseudo-classes like `:not()`, `:has()`, or `:is()` is strictly prohibited.

### 6. Dynamic States (States)
Short, semantic javascript-toggled flags starting with a leading underscore (`_act`, `_open`, `_err`).

### 7. Responsive Suffixes (Responsive)
Allowed **strictly for structural behavior** (hiding/showing, full-width snapping `-full_sm`, changing flex direction). Design variations (colors, typography, decorative shadows) on different screens must be managed inside the element's media queries in CSS.

### 8. "Flat CSS" Architecture (No Cascade)
Nesting selectors via spaces is prohibited. The baseline selector specificity weight is `0,1,0`, with strictly monitored exceptions.
**Four strict exceptions to the cascade rule:**
1. **Third-party vendor libraries** (detected by the linter via the absence of Quiql trailing/leading tokens, e.g., `.pCd_.swiper-pagination`).
2. **Functional UI micro-modules** (e.g., star ratings, custom accordion/tab logic using checkboxes) where logic depends on neighboring elements, allowing native combinators (`+`, `~`, `:checked`).
3. **Rich text containers** from a CMS/WYSIWYG editor (`.pCd_richText p`).
4. **Native interactive states** (the Hover/Focus rule) to prevent "custom properties hell" on parent-triggered pseudo-classes (`:hover`, `:focus`, `:active`, `:disabled`).

#### 🚦 The Hover/Focus Exception Explained
To avoid creating hundreds of boilerplate CSS variables for a simple mouse hover, you are allowed to use a direct parent-to-child cascade **strictly combined with a native pseudo-class**.

##### ❌ BAD (Avoid bloating CSS with variables for simple hovers):
```css
.pCd_ {
  --pCd-ttl-clr: #000;
}
.pCd_:hover {
  --pCd-ttl-clr: #ff0000;
}
.pCd_ttl {
  color: var(--pCd-ttl-clr);
}
```

#####  GOOD (Clean, fast, and optimized for browser engines):
```css
/* Specificity naturally increases to 0,3,0, which is perfectly safe for interactive states */
.pCd_:hover .pCd_ttl {
  color: #ff0000;
}
```

##### 🔐 The Prefix-Match Iron Rule (Intra-Module Protection)
To guarantee 100% encapsulation and keep the `Ctrl+F` navigation unbreakable, the interactive cascade exception is allowed **strictly within the same module**. The alias of the parent selector **must identicaly match** the alias of the child element. Inter-module cascading is hard-blocked by design.

```css
/* ✅ GOOD: Both elements belong to the same module namespace (pCd_) */
.pCd_block:hover .pCd_ttl {
  color: #ff0000;
}

/* ❌ CRITICAL ERROR: Inter-module leakage! ProductCard breaks Table isolation. */
.pCd_block:hover .tbl_ttl {
  color: #ff0000;
}
```

*   **How to solve inter-module logic:** If hovering over Component A must visually affect Component B, you must either manage this state via a common layout parent using global context CSS variables, or toggle a local dynamic state flag (`_act`) on Component B using modern JavaScript.

##### ⚠️ The Golden Rule of Quiql Cascade:
This exception applies **ONLY** to native pseudo-classes triggered by user interaction. If you are changing global component states, themes, or modifiers via JavaScript or server-side logic (e.g., toggling a `-disabled`, `-active`, or `-themeDark` modifier class), you **MUST** use CSS Variables declared on the parent element to pass the state down.

### 9. The Mix Rule (Context vs Content)
A component defines its internal design; its own outer `margin` is always 0. External layout positioning is dictated by the parent container (via `gap` or layout grid element mixes).

### 10. JavaScript Integration
DOM queries and event listeners must bind strictly to element classes (`pCd_btn`). State classes (`_act`) are only toggled and must not be used as primary search hooks. Global atoms are completely off-limits for JS logic.

### 11. Hierarchy of Layers (CSS Order)
File imports and selector declarations must strictly scale upwards. Media queries must always follow their respective base selectors.
1. **Utility Layer** (`.-mod` $\rightarrow$ `@media { .-mod_md }`)
2. **Atom Layer** (`.atom-` $\rightarrow$ `@media { .atom-.-mod_md }`)
3. **Component Layer** (`.pCd_btn` $\rightarrow$ `.pCd_btn.-mod` $\rightarrow$ `@media { .pCd_btn.-mod_md }`)

---

## 🚀 Production Example

### HTML
```html
<div class="ShopGrid_ sG_">
  <!-- Mix Rule: sG_item positions the card, pCd_ outer margin is 0 -->
  <article class="ProductCard_ pCd_ sG_itm">
    
    <!-- Element + Preset Modifier -->
    <h2 class="pCd_ttl -heroText">Quiql Phone X</h2>
    
    <!-- Structural Responsive Suffix (Hidden on mobile) -->
    <p class="pCd_dsc -hid_-sm">Eco-friendly digital layout.</p>
    
    <!-- Global Atom + Local Element Mix -->
    <button class="btn- pCd_btn -prm">Buy Now</button>
    
  </article>
</div>
```

### CSS
```css
/* Layer 2: Global Atoms */
.btn- { display: inline-flex; align-items: center; justify-content: center; }

/* Layer 3: Local Components */
.pCd_ { display: flex; flex-direction: column; background: #fff; }
.pCd_ttl { font-size: 1rem; color: #333; }

/* Modifier Chaining (Role Preset) */
.pCd_ttl.-heroText { font-size: 2.5rem; font-weight: 800; color: #ff0055; }

/* Local Atom Refinement */
.pCd_btn.-prm { background: #00ffcc; }

/* Native pseudo-classes strictly at the end */
.pCd_btn.-prm:hover { opacity: 0.9; }

/* Responsive Suffix (Structural behavior only) */
@media (max-width: 576px) {
  .pCd_dsc.-hid_-sm { display: none; }
}
```

### JavaScript
```javascript
// Bind logic strictly to the unique element class
const button = document.querySelector('.pCd_btn');

button.addEventListener('click', () => {
  // Toggle the state class seamlessly
  button.classList.toggle('_act'); 
});
```

---
🧬 **Quiql Ecosystem 2026** | Develop web with purpose.
