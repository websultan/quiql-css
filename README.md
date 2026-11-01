# 📋 Quiql CSS v1.0 — The "Golden Mean" CSS Methodology

**Quiql CSS** is an ultra-efficient architectural methodology designed for high-performance web development. It delivers exceptional results across the entire spectrum of engineering—from classic multi-page applications (HTML, PHP, Blade, CMS) to modern Single Page Applications (React, Vue, Svelte). Quiql preserves the strict encapsulation of BEM while adopting the brevity of Tailwind, radically reducing HTML/JS payload size, optimizing Virtual DOM parsing, and leveraging native CSS variables for reactive state management without losing semantics.

---

## 🎯 Why Quiql? (Problem — Solution)

Modern web development is trapped in two extremes:
* **Tailwind / Utility-first:** Offers blazing-fast development speed but results in an unmaintainable, bloated HTML carcass packed with thousands of chaotic, repetitive utility classes.
* **BEM / Semantic CSS:** Provides a clean DOM tree and strict architecture but suffocates developers with endless naming bureaucracy, massive CSS file sizes, and agonizingly slow writing speeds.

**Quiql CSS is the third way.** It delivers the atomic speed of utility frameworks directly inside predictable component structures, using ultra-short tokens. You write styling at the speed of thought, keeping the CSS tiny, the HTML clean, and global searching (`Ctrl+F`) fully native.


### Why Lightweight HTML Matters More Than Compression (The Runtime Overload)

Modern web development suffers from a common misconception: *"HTML bloat doesn’t matter because Gzip/Brotli will compress it anyway."*

While compression optimizes network transfer, it only deceives the wire—**it cannot deceive the user's browser, the device RAM, or the server's CPU.** Furthermore, their lifecycles differ fundamentally: CSS is cached **once**, while HTML is generated and downloaded from scratch **on every single page transition or refresh**.

#### 1. Client-Side Optimization: CPU vs. Network

When a browser receives compressed HTML, it executes a heavy execution chain:
`Download Archive` → `Decompress (CPU)` → `Parse DOM Tree` → `Style Recalculation`.

* **The Illusion:** A Tailwind-built page weighs **421 KB**, and network compression squeezes it to **~40–95 KB**. The network stage finishes quickly.
* **The Runtime Reality:** Once inside the device, the CPU decompresses the file back to its full **421 KB** size in RAM.
* **The Bottleneck:** Mobile processors cannot parse compressed strings. The CPU wastes clock cycles reading thousands of repetitive utility classes (e.g., `class="max-w-sm rounded-xl overflow-hidden..."`). This blocks the **Main Thread**, causing micro-stutters and directly degrading Google's Core Web Vitals—specifically the **INP** (*Interaction to Next Paint*) metric.

##### Real-World Case Study: Tailwind vs. Quiql CSS
Audit of a production e-commerce store page (`https://demo.laravelshopper.dev/store`) running 1,030 elements:

| Metric | Tailwind CSS | Quiql CSS (Calculated) | Net Impact |
| :--- | :--- | :--- | :--- |
| **Raw HTML Size (Uncompressed)** | **421 KB** | **263.9 KB** | **~37.3% lighter DOM in RAM** |
| **Network Size (Compressed)** | **~40–95 KB** | **~15–35 KB** | **Faster Time to First Paint** |
| **Pure Class Strings Weight** | **188 KB (44.6%)** | **30.9 KB** | **83.5% reduction in class bloat** |
| **Average Class Length** | ~186 chars / tag | ~30 chars / tag | Clean, ultra-short markup |

**The quiql-css Solution:** By enforcing short architectural tokens (aliases like `prCd_` and flat elements like `prCd_ttl`), the markup skeleton weighs up to **83% less than Tailwind** in class attribute footprint. The browser parses this lightweight DOM instantaneously without RAM overhead, while global **Beacons** (`ProductCard_`) preserve full code searchability (`Ctrl+F`).

#### 2. The Duplicate Weight of SSR Hydration

If your stack uses **Next.js, Nuxt, Remix, or Astro**, your markup data is inherently sent to the client **twice** within a single server response:
1. As a rendered HTML layout for the initial paint.
2. Inside a hidden `<script>` tag as a massive JSON state object (`__NEXT_DATA__` or equivalent) for JavaScript hydration.

When components are cluttered with long utility strings, this textual waste is **duplicated twice** in the payload. For large-scale apps, this multiplies into megabytes of pure overhead. The compact structural system of `quiql-css` slashes this footprint in both locations simultaneously.

#### 🌳🎁 The Safety Net & GreenIT: What if Compression Fails?

Network compression frequently breaks or is intentionally disabled due to corporate proxy misconfigurations, legacy edge hosting, or strict fintech security policies (mitigating BREACH attacks).

Without compression, networks choke on Tailwind HTML. With compression, servers waste millions of CPU cycles archiving data on-the-fly. `quiql-css` fixes the root cause directly at the source code level.

At **1,000,000 page views per day** on an uncompressed MPA architecture (Laravel Blade, Shopify Liquid, WordPress), eliminating this raw textual waste saves:
* **57.3 Terabytes** of raw network traffic per year.
* **9,188 kWh of electricity** (enough to power an average residential apartment for 4 consecutive years).
* **4,051 kg of CO₂ emissions** (equivalent to the carbon offset absorbed by 183 mature trees per year).

**Summary:** `quiql-css` proves that the most sustainable code is efficient by design. Instead of spending datacenter and mobile hardware energy on redundant *compress-on-server → decompress-on-client* cycles, we simply eliminate the garbage before it hits the engine.

---

## 📊 Syntax Cheatsheet (Unique Architecture Tokens)

Thanks to its strict token system, Quiql is 100% predictable for developers and effortlessly validated by automated linters.

| Entity | Architectural Token | Class Example | Purpose |
| :--- | :--- | :--- | :--- |
| **Beacon** | `[beacon]_` (in CSS as a comment) | `ProductCard_` | Global `Ctrl+F` navigation locator |
| **Alias** | `[alias]_` (ultra-short component name)| `prCd_` | Local module namespace isolation |
| **Element** | `[alias]_[element]` | `prCd_title` | Flat component structure element |
| **Atom** | `[atom]-` (trailing hyphen) | `btn-`, `img-` | Global system-wide layout constructors |
| **Modifier** | `-[modifier]` (leading hyphen) | `-promo`, `-bold`| Role-based style presets |
| **State** | `_[state]` (leading underscore) | `_active`, `_opened` | Dynamic state flags toggled via JS |
| **Responsive Utilities** | `-[utility]_-[breakpoint]`<br>`-[utility]_[breakpoint]`<br>`-[utility]_[breakpoint]-` | `-hid_-sm`<br>`-full_xl`<br>`-rev_md-` | Structural responsive behavior only |

> ⚠️ **Strict Naming Constraint:** The **Beacon** is the *only* entity written in `PascalCase`. All other token sub-components, element names, modifiers, and state words **must strictly use `camelCase`** for multi-word separation. Underscores (`_`) and hyphens (`-`) are strictly reserved as system architectural delimiters and must never be used as text word spacers.

### 📖 The Controlled Dictionary Rule

To maximize HTML payload reduction and maintain a unified coding dialect across teams, you can use short aliases—but **strictly from the official Quiql Dictionary** to use the standard tokens listed below for common UI elements.

If an element is not present in the official dictionary, its name must be written in full (e.g., `prCd_gallery` or `prCd_balance`). Inventing custom, non-standard abbreviations is forbidden to prevent code fragmentation and preserve immediate readability for new developers.

| Full Word | Quiql Token | Full Word | Quiql Token |
| :--- | :--- | :--- | :--- |
| Title | `ttl` | | |
| Text | `txt` | Description | `desc` |
| Wrapper | `wrp` | Column | `col` |
| Button | `btn` | Link | `lnk` |
| Label | `lbl` | Input | `inp` |
| Image | `img` | Background | `bg` |
| List | `lst` | Item | `itm` |
| Primary | `prm` | Secondary | `sec` |
| Success | `suc` | Error | `err` |
| Hidden | `hid` | Visible | `vis` |
| Full-width | `full` | Reverse | `rev` |
| Small (Mobile) | `sm` | Medium (Tablet) | `md` |
| Large (Desktop)| `lg` | Extra Large | `xl` |

---

## 📜 The Quiql CSS Manifest (11 Core Rules)

### 1. Block Declaration (The Beacon)
Written in `PascalCase_` strictly at the root element of the HTML component, and **exclusively as a comment** in CSS (`/*! ProductCard_ */`). It is used solely as a "beacon" for global project search (`Ctrl+F`) and does not carry any styles.

### 2. Component Alias (The Namespace & Parent)
The working name of the component used for styling in CSS, written in `camelCase_`. The bare alias (without additional words) strictly targets the **parent (root) element** of the component for styling.

To keep HTML ultra-lightweight and ensure predictable names, the alias is generated directly from the Beacon using the strict **Aliasing algorithm**:

#### 📐 The 4 Rules of Aliasing

1. **Casing & Capitalization**
   The first letter of the alias is **always lowercase**. For multi-word components, every subsequent word inside the alias maintains its capital letter to preserve structural boundaries.
   * *Examples:* `Header_` → `hdr_`, `FooterMenu_` → `ftMn_`, `WeWon1Place_` → `weWn1Pc_`

2. **1 and 2-Letter Words (No Compression)**
   Words or individual letters consisting of 1 or 2 characters are never compressed or mutated.
   * *Examples:* `IPhone_` → `iPn_` (lowercase `i` + compressed *Phone*), `We_` → `we_`, `ContactUs_` → `cnUs_`

3. **3-Letter Words (Conditional)**
   Left uncompressed **only** if it is a single-word component. Otherwise, it follows standard reduction.
   * *Examples:* `Ban_` → `ban_`, `Who1_` → `wh1_`, but `WhyWe_` → `whWe_`

4. **Standard 2-Character Reduction (4+ Letters)**
   Each word shrinks to exactly 2 characters. Non-final words take **first letter + next consonant**. The absolute final word takes **first letter + last consonant**.
   * *Examples:* `Navigation_` → `nvn_`, `PostCard_` → `psCd_`, `ProductPrices_` → `prPs_`
   * *Vowel Rule:* If a word lacks consonants, use the first available vowel: `SeaTrip_` → `seTp_`, `FriendOrFoe_` → `frOrFo_`
   *  **Vowel Rule Edge Cases (Short Single-Word Components):**
      If a single-word component consists of only 3 to 4 letters and severely lacks consonants for standard reduction, the alias is generated using a strict linear sequence:
      Formula: `[First Letter] + [Next Available Character (Vowel or Consonant)] + [Final Consonant]`.
      * *Examples:* `Area_` → `are_` (a + r + e), `Wood_` → `wod_` (w + o + d), `Ice_` → `ice_` (i + c + e).
      * *Note:* When these same words are used inside **multi-word** components, they always shrink back to the standard 2-character layout (`AreaTrip_` → `arTp_`, `WoodBox_` →  `wdBx_`).

#### 🛡️ Collision Resolution (MPA-first)
If a generated alias already exists, it triggers a collision. The existing (older) component retains priority. For manual MPA development, **adding a sequential number is the primary recommended fix**. Alternatively, you can expand the word backward from the end.
* **Standard Alias:** `prPs_` (*ProductPrices*)
* **Primary Fix (Number):** `prPs2_` (Fastest to read and write)
* **Alternative Fix (Word Expansion):** `prPes_` → `prPcs_` (Restoring *Pri-c-e-s* backward)

Any alias containing digits or 3+ characters in a word instantly signals a manually resolved collision. *(Note: Automated hash-based resolution like `prCd0d` is planned for the upcoming SPA toolchain).*

### 3. Child Elements (Structure)
Elements inside the component are created by appending a **Structure word** directly to the alias. It is recommended to use tokens from the official dictionary, but developers are free to use custom words if the required semantic role is missing.

* **Syntax:** `[alias]_[word]` (e.g., `usCd_ttl`, `mHdr_btn`, `usCd_customWord`).
* **Flat Architecture:** Quiql avoids deep nesting syntax (like BEM's `__`). All child elements remain flat within the namespace, regardless of their visual or structural depth in the HTML tree.
* **Strict Meaning:** A structure word defines *what* the element is (its semantic role), not *how* it looks.

### 4. Global Atoms (Atoms)
System-level layout and UI primitives (`btn-`, `inp-`). The Atom provides the global base; the local element handles component-specific overrides (`class="prCd_btn btn-"`).
*   **Atom Autonomy:** Global Atoms are strictly systemic, indivisible primitives. They do not possess child elements and never follow the Beacon aliasing algorithm.

### 5. Modifiers, Presets & Component Pseudo-classes (Modifiers)
Set during page rendering to represent a fixed alteration; must not change or disappear during the session. Use encapsulated role presets (`-promo`) instead of utility-first class bloating (`-red -bold -sizeLg`).
* **Global vs. Local Modifiers:** Modifiers can be local (deeply encapsulated within a single module namespace) or global (system-wide tokens applied across multiple components, e.g., `-bold`, `-red`).
* **The Antidote to Bloat:** Global modifiers must be used strictly as rare, systemic exceptions. Combining multiple global modifiers on a single tag to mimic utility-first frameworks is strongly discouraged. If an element requires more than two visual alterations, they must be refactored into a single local role preset.
* **Chaining (No Cascade):** Individual modifiers must be defined separately. Chain selectors without spaces strictly to resolve modifier intersections. In CSS, these chains **must be written in alphabetical order**: `.prCd_btn.-promo.-sec`.
* **Advanced Selectors (`:has`, `:is`, `:where`, `:not`):**
  * **Allowed:** Parent tracking using `:has()` on parent elements (e.g., `.prCd:has(._err)`); grouping modifiers or structural elements via `:is()` or `:where()` is permitted freely to keep code DRY.
  * **⚠️ Strongly Discouraged for Modifiers:** Using `:not()` to exclude modifiers or component classes (e.g., `.prCd_btn:not(.-promo)`).

> 💡 **Why avoid `:not()` for component modifiers?**
> It creates inverted logic that is harder to read. More importantly, it violates the open-closed principle: if you add a new modifier (e.g., `.-sale`) in the future, the `:not(.-promo)` rule will automatically apply to it, which often leads to unexpected layout bugs. Stick to standard cascade overrides instead.
>
> 🛠️ **`:is()` vs `:where()` Tip:**
> Remember that `:is()` takes the specificity of its most specific argument, while `:where()` **always has 0 specificity (`0,0,0`)**. Use `:where()` if you want to create baseline styles for a group of modifiers that must be easily overridden later without fighting the cascade.

### 6. Dynamic States (States)
Short, semantic javascript-toggled flags starting with a leading underscore (`_active`, `_opened`, `_err`).
Managed by the UI logic to reflect a runtime status; can freely appear or disappear on the fly.

### 7. Global Responsive Utilities (Responsive Vectors)

#### 🎯 Purpose & Architectural Limitations
Global responsive utilities in Quiql CSS are allowed **strictly for structural behavior** and layout direction (e.g., hiding `-hid_-sm`, full-width snapping `-full_md-`, shifting flex direction `-row_-md`, `-col_sm`, or reversing it `-rev_lg-`). These utilities are structured as modifiers and apply exclusively to static variations. Dynamic state classes (States) must never use responsive suffixes; any screen-specific state behavior (e.g., active or open states on different devices) must be managed inside the element's media queries in CSS.

#### 📐 The Three Adaptive Vectors & Breakpoint Math
Quiql CSS does not enforce rigid, hardcoded screen dimensions; teams are free to define their own custom breakpoint values (e.g., `sm`, `md`, `lg`, `xl`) depending on the project's design grid.

However, to prevent screen overlapping and eliminate the "1px dead zone gap" on high-density Retina or scaled displays, the responsive system must strictly implement the three-vector token syntax based on a precise `0.02px` mathematical subtraction rule:

* **`-[utility]_-[breakpoint]` (The Left Vector / `max-width`)**
  Targets all screens strictly **smaller** than the starting boundary of the specified breakpoint.
  *Formula:* `@media (max-width: [breakpoint-value] - 0.02px)`
  *Example:* `-hid_-md` — hidden everywhere below the `md` start line.
* **`-[utility]_[breakpoint]-` (The Right Vector / `min-width`)**
  Targets all screens **starting from** the specified breakpoint and larger (the core Mobile First engine).
  *Formula:* `@media (min-width: [breakpoint-value])`
  *Example:* `-row_md-` — becomes a flex-row strictly from `md` up to desktop.
*   **`-[utility]_[breakpoint]` (The Interval Vector / Target Screen Only)**
  Targets **only** the unique range of that specific device tier, safely bounded before the next larger breakpoint begins.
  *Formula:* `@media (min-width: [current-breakpoint]) and (max-width: [next-breakpoint] - 0.02px)`
  *Example:* `-full_md` — snaps to full-width exclusively on tablets (`md`), maintaining its normal component dimensions on both mobile phones and large desktops.

#### ⚖️ The Cleanliness Trade-Off: Utilities vs. Pure CSS

Global responsive utilities are strictly **optional**. While they speed up layout assembly, overusing them (e.g., `class="prCd_desc -hid_-sm -full_md -row_lg-"`) re-introduces the HTML bloat we built Quiql CSS to destroy.

Developers are free to choose between two architectural paths depending on project priorities:

1. **The Utility Fast-Track (DX Priority):** Use responsive utility suffixes directly in HTML for fast layout variations. This is ideal for rapid prototyping or generic structural blocks.
2. **The Pure CSS Track (HTML Payload Priority):** Completely eliminate utility classes from the HTML carcass to achieve a 100% lightweight DOM. All screen-specific variations are encapsulated directly inside the component's CSS block using local media queries:

```html
<!-- 🟢 The Pure CSS Approach: ZERO utility bloat in HTML -->
<p class="prCd_desc">Eco-friendly digital layout.</p>
```

```css
/* Clean, encapsulated local media query fallback */
.prCd_desc {
  display: block;
}
@media (max-width: 575.98px) {
  .prCd_desc {
    display: none;
  }
}
```

### 8. The Declaration-Driven Contract (Variables & Animations)
To completely eliminate cognitive load, ensure absolute local scoping, and guarantee 100% code traceability, the names of both **custom properties (CSS variables)** and **animations (`@keyframes`)** must be derived directly from the exact architectural token to which they semantically belong.

#### 📐 Part 1: CSS Variables Syntax (`--[token]-[propertyName]`)
*(Declared directly inside the corresponding CSS selector block)*
*   **Root Component Element:** `--prCd_-color` (declared inside `.prCd_`)
*   **Child Element:** `--prCd_ttl-color` (declared inside `.prCd_ttl`)
*   **Global Atom:** `--btn--color` (declared inside `.btn-`)
*   **Modifier:** `---accent-color` (declared inside `.-accent`)
*   **State:** `--_active-color` (declared inside `._active`)
*   **External Interface Ports (Black Box):** When a component creates a variable designed to be read by nested external modules, a trailing hyphen **must** be appended to the end of the variable name: `--[parentToken]-[propertyName]-` (e.g., `--prCd_-color-`).

#### 📐 Part 2: Scoped Animations Syntax (`[token]-[animationName]`)
*(Declared independently at the stylesheet root level, then referenced via `animation-name` inside the selector)*
*   **Root Component Element:** `prCd_-fade` (scopes the entire card layout transition)
*   **Child Element:** `prCd_ttl-pulse` (scopes a specific typography element movement)
*   **Global Atom:** `btn--blink` (system-wide architectural animation primitive)
*   **Modifier:** `-promo-shake` (animation behavior tied strictly to a visual preset)
*   **State:** `_active-bounce` (runtime micro-interaction triggered via JavaScript state)

> 💡 **The Ultimate Traceability Contract:** This explicit pairing enforces a flawless global search (`Ctrl+Shift+F`) experience. Searching for any element token (e.g., `prCd_ttl`) instantly displays its HTML tag node, its core layout CSS block, its custom design tokens (`--prCd_ttl-color`), and its isolated root-level animation behavior (`@keyframes prCd_ttl-pulse`) within 2 seconds.

### 9. "Flat CSS" Architecture & The Interaction Contract

Nesting selectors via spaces is prohibited. The baseline selector specificity weight is strictly kept at a flat `0,1,0`. To maximize development speed (DX) without causing specificity wars or breaking encapsulation, all parent-to-child style overrides must strictly follow the Quiql Interaction Matrix.

#### 🎛️ Part 1: Inter-Module Interactions (The Black Box Contract)
When a parent component needs to visually alter a **different, independent component** nested inside it (which uses a completely different alias prefix), **cascading via spaces is strictly forbidden**. You must interact exclusively through an Interface Token acting as a "Black Box" port.
*   **The Rule:** Only CSS variables named after the parent. The parent modifies this external token on interaction, while the independent child component consumes it strictly as a safe native fallback.

```css
/* CHILD COMPONENT: Rating (rating.css) */
.rtg_itm {
  color: var(--prCd_-color-, rgba(240, 211, 46, 0.7));
}

/* PARENT COMPONENT: Product Card (product-card.css) — CASCADING IS FORBIDDEN */
.prCd_.-full {
  --prCd_-color-: rgba(255, 215, 0, 1); /* Safely shifts the child module's environment */
}
```

#### 🟢 Part 2: Intra-Module Connections with Low Specificity (Weight <= 0,3,0)
When a trigger (hover, state, modifier) on a parent needs to alter its own descendant elements (sharing the exact same module alias prefix) and the final selector weight does not exceed `0,3,0`.
*   **The Rule:** Use standard **native cascading via spaces** — it is the simplest, most performant, and fastest way for the browser runtime. However, if you prefer a declarative approach using **local variables**, you may use them at your discretion.

```css
/* ✅ Simple, performant, and fast cascade via spaces (Specificity 0,3,0) */
.prCd_ttl._err .prCd_ttlPart {
  color: red;
}

/* ☝️ Alternative via local variables (perfectly valid if preferred) */
.prCd_ttl._err {
  --prCd_ttl-partColor: red;
}
.prCd_ttlPart {
  color: var(--prCd_ttl-partColor, black);
}
```

#### 🟡 Part 3: Complex Intra-Module Connections (Weight > 0,3,0)
When multiple modifiers and interactive pseudo-classes intersect on the exact same tag (e.g., `.prCd_.-promo._active:hover`, naturally yielding `0,4,0`), blowing past the architectural specificity cap.
*   **The Rule:** Wrap the interactive pseudo-class inside the zero-specificity **`:where()` or `:is()`** blocks—this is the simplest and cleanest way to keep the selector weight at `0,3,0` while ensuring optimal browser rendering performance.
*   **Exception:** If the project requires **legacy browser support** where `:where()` is unavailable, bypass the selector entirely by shifting values via component-level **CSS variables**.

```css
/* ❌ Forbidden (0,4,0) — Exceeds the core architecture cap */
.prCd_.-promo._active:hover {
  background: gold;
}

.inp-:checked + .inpBox-.-prm {
  border-color: #000;
}

/* ✅ Approved "Simpler" Way (0,3,0) — Keeps state weight flat and fast via :where() */
.prCd_.-promo._active:where(:hover) {
  background: gold;
}

.inp-:checked + .inpBox-:where(.-prm) {
  border-color: #000;
}

/* 🛠️ Approved "Compatibility" Way — Shifting variables if legacy browsers are targeted */
.prCd_.-promo {
  --prCd_-bgHover: gold;
}
.prCd_._active:hover {
  background: var(--prCd_-bgHover);
}

.inp-:checked {
  --inp--bg: #000;
}
.inpBox-.-prm {
  border-color: var(--inp--bg, transparent);
}
```

#### 🗂️ Part 4: Native Cascade Exceptions (Legacy & Third-party)
Direct structural cascading via spaces and native combinators is permitted **strictly** within these three isolated engineering scenarios:
1.  **Third-party vendor libraries:** Modifying deep plugin layouts where Quiql classes are mixed with vendor selectors (e.g., `.prCd_sliderVirtual.swiper-virtual.swiper-css-mode .swiper-wrapper::after`). However, if you use `@layer`, you can avoid heavy cascading altogether. Simply wrap the third-party library inside a weak native layer via the `@import` function:
    ```css
    @layer qVendor;
    @import "swiper/css" layer(qVendor);
    ```
    This confines the library's styles to a lower priority tier, allowing you to easily override any deep vendor layout using standard flat Quiql classes without breaking the architecture.

2.  **Rich text containers:** Styling raw, unpredictable HTML output from a CMS or WYSIWYG editor (e.g., `.prCd_richText p`, `.prCd_richText ul li::before`).

### 10. The Mix & Layout Rule (Context vs Content)
A component exclusively defines its internal design and behaves as a flexible container. The component's base selector, **as well as any Global Atom**, must maintain strict layout independence: they must have `margin: 0`, avoid fixed, non-fluid dimensions (never use `width` or `height` in explicit `px` or `rem`), and never enforce outer flow positioning (`position: absolute/fixed/sticky`, `top`, `left`, `z-index`, etc.). External layout positioning and outer dimensions are always dictated by the **external context**.

#### 📐 Three Approved Methods for Component & Atom Positioning:

1. **Parent Layout Container (Grid & Gap)**
   The parent container manages the grid system and gaps via native CSS `gap`, `grid`, or `flex` properties. Components and Atoms placed inside simply conform to the grid structure. Every component root alias is strictly paired with its Beacon.
   ```html
   <div class="ShopGrid_ shGd_">
     <article class="ProductCard_ prCd_"></article>
   </div>
   ```

2. **Architectural Mix (BEM-style Mix)**
   The component's or atom's tag is mixed with a structural element belonging to the parent container. The Beacon is placed exclusively before the component's own alias. Outer layout properties (`margin`, `width`, `position`, etc.) are written **strictly inside the parent's element selector** in CSS.
   ```html
   <!-- prCd_ is pure content layout. shGd_itm defines the context grid cell -->
   <article class="ProductCard_ prCd_ shGd_itm"></article>
   
   <!-- Atom Mixed with a parent layout element -->
   <button class="btn- shGd_actBtn"></button>
   ```
   ```css
   /* atoms.css */
   .btn- {
     background: #fff; /* Safe: no margin or rigid width here */
   }

   /* ProductCard.css */
   .prCd_ {
     background: #fff; /* Safe: no margin or rigid width here */
   }
   
   /* ShopGrid.css */
   .shGd_itm,
   .shGd_actBtn {
     margin-bottom: 2rem; /* Safe: outer positioning handled by the parent */
     position: absolute;  /* Context-specific placement */
     top: 10px;
   }
   ```

3. **Context Modifier (The Individual Exception)**
   If a component or an atom requires a one-off structural shift or positioning adjustment without using an architectural mix or parent grid, a dedicated layout modifier is permitted.
   
   *⚠️ Strict Limitation:* Atomized utility style modifiers (Tailwind-like approach) are **strongly discouraged** and must be avoided. They are permitted exclusively as a last resort in extreme, isolated layout edge cases to prevent class-attribute bloat and preserve module encapsulation.
   ```html
   <article class="ProductCard_ prCd_ -marginTopLg"></article>
   <button class="btn- -marginTopLg"></button>
   ```

#### 🚫 The Official Layout Property Blacklist

To strictly enforce encapsulation and prevent layout breakage, the following CSS properties are **strictly prohibited** when targeting a component's base selector (e.g., `.prCd_`) or a global atom (e.g., `.btn-`):
*   ❌ **Strictly Forbidden (Complete Lock):** `margin` (including all directional sub-properties), `top`, `right`, `bottom`, `left`, and `z-index`.
*   ❌ **Forbidden for Component Roots:** `position: absolute`, `position: fixed`, and `position: sticky`.
*   🟢 **Explicitly Allowed:** `position: relative` (permitted exclusively to establish a local stacking context for internal absolute child elements) and `position: static`.
*   📐 **Dimensional Restrictions:** Rigid, hardcoded dimensions (e.g., `width: 450px` or `height: 600px`) are forbidden on root selectors. Components must remain fluid, utilizing only `100%`, `auto`, `min-content`, `max-content`, or `fit-content`.
    * *Exception:* Hardcoded dimensions in `px` or `rem` are allowed **strictly for graphical primitives** whose anatomy never alters regardless of context (e.g., icons, avatars, checkboxes).

### 11. Hierarchy of Layers (HTML & CSS Order)

Excluding initial base styles (Normalize, Reset, and native tag styling), all Quiql CSS architectural entities must follow a strict upward-scaling hierarchy both in markup attributes and stylesheets. Dependent styles (Modifiers and States) must strictly follow their respective base templates to ensure predictable cascade behavior.

#### 📐 Part 1: HTML Class Token Ordering Rule (Outside-In Sequence)

To guarantee absolute predictability, instant visual scanning of the DOM tree, and clean JS DOM mutations, all architectural tokens within the HTML `class="..."` attribute must strictly follow the linear sequence from External Context to Runtime Dynamics:
`[New Component Beacon & Alias] → [Parent Mix Element] → [Global Atom] → [Modifiers] → [Responsive Utilities] → [Dynamic States]`

* **New Component Beacon & Alias:** Opens the module boundary if the tag serves as a root element (`Accordeon_ acn_`).
* **Parent Mix Element:** Defines the node's position inside the parent container context (`prCd_faq`).
* **Global Atom:** Declares the universal base anatomy of the element (`box-`).
* **Modifiers:** Applies static design role presets (`-prm`).
* **Responsive Utilities:** Injects adaptive structural behavior restrictions (`-hid_-sm`).
* **Dynamic States:** Holds dynamic javascript-toggled runtime flags (`_active`). Placed strictly at the end for immediate searchability and seamless `classList` mutations.

*Correct HTML Syntax Order:*
```html
<div class="Accordeon_ acn_ prCd_faq box- -prm -hid_-sm _active"></div>
```

#### 🗂️ Part 2: The Official CSS Layer Sequence (Top to Bottom)

1. **Global Utility & Modifier Layer (The Structural & Global Presets)**
   * Global Utilities (`.-hid_-sm` — structural classes with `!important`).
   * Global Role Modifiers (`-prm`, `-sec` — application-wide design tokens).
   * Global System States (`_active`, `_vis` — global dynamic flags toggled on layout roots).
   
2. **Atom Layer (Global Layout Constructors)**
   Must be declared in a strict internal hierarchy:
   * Base Atoms (`.btn-`, `.grid-`).
   * Atoms Pseudo-elements (`.btn-::before`, `.btn-::after`).
   * Atom + Modifier intersections (`.btn-.-prm`).
   * Atom Pseudo-classes / Hovers (`.btn-:hover`, `.inp-:focus`).
   * Atom + Runtime State intersections (`.btn-._active`).
   * Atom + Modifier + State combined chains (`.btn-.-prm._active`).
   * Atom Media Queries (All media queries targeting atoms must follow right after this entire block).

3. **Component Layer (Encapsulated Modules)**
   Mirrors the same predictable internal hierarchy as the Atom Layer:
   * AI-Ready Production Beacon as a comment (`/*! ProductCard_ */`).
   * Base Components & Child Elements (`.prCd_`, `.prCd_ttl`).
   * Component Pseudo-elements (`.prCd_ttl::before`, `.prCd_ttl::after`).
   * Component + Modifier intersections (`.prCd_ttl.-heroText`).
   * Element Pseudo-classes / Hovers (`.prCd_ttl:hover`).
   * Component + Runtime State intersections (`.prCd_btn._active`).
   * Component + Modifier + State combined chains (`.prCd_btn.-prm._active`).
   * Parent-driven Cascades / Context States (`.prCd_:hover .prCd_txt`).
   * Component Media Queries (All local responsive behavior follows right after this module block).

#### 📐 Responsive Cascade Sequence
Inside the Global Utility Layer, media queries must follow a strict three-stage mathematical sequence to guarantee a safe cascading fallback if a developer accidentally mixes conflicting classes in HTML:

1. **Left Vectors (`max-width`):** Sorted from largest to smallest breakpoint to allow narrower rules to override wider ones safely.
2. **Interval Vectors (`min-width` and `max-width`):** Sorted sequentially from smallest to largest tier. Since these ranges are mathematically isolated by the `0.02px` rule, they do not overlap.
3. **Right Vectors (`min-width`):** Sorted from smallest to largest breakpoint, powering the core Mobile First engine by allowing larger display rules to naturally override mobile defaults.

---

## 🚀 Production Example (Full Stack Showcase)

To achieve maximum HTML weight reduction, this example heavily utilizes tokens from the **Quiql Controlled Dictionary** (`ttl`, `desc`, `btn`).

### 📄 HTML Layout
```html
<div class="ShopGrid_ shGd_">
  <!-- 1. Layout Mix: 'shGd_itm' positions the card. The card's root ('prCd_') margin is strictly 0 -->
  <article class="ProductCard_ prCd_ shGd_itm">
    
    <!-- 2. Flat Element + Role Preset Modifier -->
    <h2 class="prCd_ttl -heroText">Quiql Phone X</h2>
    
    <!-- 3. Structural Responsive Suffix (Element hides strictly on mobile screens) -->
    <p class="prCd_desc -hid_-sm">Eco-friendly digital layout engineering.</p>
    
    <!-- 4. Global Atom + Local Element Mix -->
    <button class="prCd_btn btn- -prm">Buy Now</button>
    
  </article>
</div>
```

### 🎨 Pure CSS (Flat Architecture)
```css
/* Layer 1: Global Utilities & Responsive Vectors */
@media (max-width: 575.98px) {
  .-hid_-sm {
    display: none !important; /* Allowed strictly for global structural utilities */
  }
}

/* Layer 2: Global UI Atoms (Primitives) */
.btn- {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  border-radius: 8px;
  transition: opacity 0.2s;
}

/* Layer 3: Local Component Modules */
/*! ProductCard_ */
.prCd_ {
  display: flex;
  flex-direction: column;
  background: #fff;
}

.prCd_ttl {
  font-size: 1rem;
  color: #333;
}

/* Modifier Chaining (Enforcing alphabetical order for linter predictability) */
.prCd_ttl.-heroText {
  font-size: 2.5rem;
  font-weight: 800;
  color: #ff0055;
}

/* Local Atom Refinement (Stitch global primitive to the local design context) */
.prCd_btn.-prm {
  background: #00ffcc;
  color: #000;
}

.prCd_btn.-prm:hover {
  opacity: 0.9;
}

/* Runtime Dynamic State Interaction */
.prCd_btn._active {
  background: #ff0055;
  color: #ffffff;
}
```

### ⚡ JavaScript (Predictable Interactions)
```javascript
// Bind logic strictly to the unique, ultra-short element token
const button = document.querySelector('.prCd_btn');

button.addEventListener('click', () => {
  // Toggle the dynamic state class seamlessly.
  // It will mutate predictably at the very end of the class attribute string.
  button.classList.toggle('_active');
});
```

💡 **Why is this highly readable?**
Even though the classes are extremely short, the global **Beacon** (`ProductCard_`) explicitly declares the context at the very root of the component. Inside this component, any developer instantly understands that `prCd_ttl` means *Product Card Title*, and `prCd_desc` means *Product Card Description*, eliminating any cognitive load while keeping the runtime HTML payload incredibly lightweight.

---

## 🔮 Future Ecosystem: SPA Toolchain Roadmap (Vite / PostCSS)

To completely eliminate manual routine and provide an elite Developer Experience (DX) in modern component-driven frameworks (React, Vue, Svelte), the upcoming Quiql CSS toolchain will introduce automated compilation and transformation layers:
  
* **Automatic Collision Resolution**
  The toolchain will automatically generate aliases from global Beacons. If an alias collision occurs within a massive project, the compiler will instantly append a short, deterministic hash suffix, completely mitigating naming conflicts without bloating the production code.

* **Context-Aware Element Expansion**
  The compiler will automatically detect the active component module scope, allowing developers to write local structural components using ultra-short syntax. The toolchain will seamlessly expand these into full, explicit, and isolated class names during the build step.
  
* **Automated Property Scoping**
  Eliminates cognitive load when managing local custom properties. The toolchain will automatically scope and map short local variables to their specific element declaration context, ensuring full module encapsulation and safe cross-element usage without variable leakage.
  
* **Automated Specificity Clamping via `:where()`**
  The compiler will act as a strict architectural guardian. If an intersecting selector naturally exceeds the architectural specificity cap (e.g., matching multiple states and modifiers simultaneously), the toolchain will automatically wrap interactive pseudo-classes inside `:where()` to strictly clamp the selector weight down to a flat `0,3,0`.
  
* **Hardcore Performance Optimization**
  An extreme compression tier where production element classes shrink down to single-letter tokens. To preserve absolute maintainability, a lightweight client-side script will dynamically expose full semantic names into a temporary debugging layer inside the browser DevTools inspector on demand, leaving production HTML unbloated.

---

## 💬 Frequently Asked Questions & Criticism (FAQ)

### 🧠 Readability & Developer Experience (DX)

#### ❓ Won't the code turn into an unreadable "bird language" due to all the abbreviations?
**Answer:** No. The algorithm compresses strictly the **Beacon**—the name of the component itself (`ProductCard_` $\to$ `prCd_`). Since the Beacon is always declared in the HTML directly on the root tag right next to its alias, the context is immediately obvious. Internal elements are either compressed strictly according to the RECOMMENDED dictionary (`ttl`, `btn`, `img`) or written out in full (`prCd_description`). Custom, rogue abbreviations are completely forbidden.

#### ❓ Why should I learn Quiql rules in the era of Scoped CSS and CSS Modules?
**Answer:** Tools like Scoped CSS prevent style leakage to the outside, but they do absolutely **nothing to organize the code inside the component**, allowing pure chaos in selectors. Furthermore, they fail at contextual intersections, forcing developers to rely on hacky workarounds like `::v-deep`. Quiql CSS provides strict structure inside the module, completely eliminates deep cascading, and doesn't bloat the HTML with unique dynamic hashes.

#### ❓ How do new developers adapt to such a strict discipline?
**Answer:** Faster than in Tailwind or BEM, thanks to the complete elimination of variance. In Tailwind, a single button can be styled using 50 different combinations of utility classes; in BEM, it can be done via a dozen different cascades. In Quiql CSS, there is always only one correct path—it is rigidly dictated by the alias generation rules and the element dictionary. Code review becomes binary and takes seconds.

### 🏗️ Architecture & Maintainability

#### ❓ Won't the 0,3,0 specificity cap cause an explosion of variables in complex designs?
**Answer:** No. Enforcing a strict upper bound on specificity is the only way to keep CSS flat and predictable. Managing styles via root variables is a declarative approach. Complex scenarios (e.g., hovering over a card to change its title color) are elegantly handled within the `0,3,0` cap by combining modifiers and context beacons: `.prCd_:hover .prCd_ttl`. Furthermore, this rule applies strictly to inter-module interactions. In all other cases, you can freely use `:is()` and `:where()`, which allow you to write rules without using variables at all.

#### ❓ Are inter-module connections via CSS variables like `--prCd_-hoverColor-` an implicit coupling? What if the connection breaks?
**Answer:** Quiql replaces a chaotic cascade (e.g., `.prCd_:hover .rtg_star`) with an **explicit interface contract** via variables prefixed with the component name (e.g., `--prCd_-hoverColor-`). If you refactor a module, you are fully insulated from "silent breakages": a simple global search (`Ctrl+Shift+F`) for the `--prCd_-hoverColor-` variable instantly reveals all external control points within 2 seconds.

#### ❓ What if a component is deleted but its variable ports remain in the parent's styles? Will the project get bloated with dead code?
**Answer:** Unlike BEM, where a cascade tightly binds a parent and child, in Quiql CSS an unused port becomes instantly visible thanks to its prefix. Any basic linter or a careful eye during code review (especially before deleting a component) will immediately flag the error: *"The parent styles declare the variable `--prCd_-hoverColor-`, but no module is using it."*

#### ❓ Why are there no IDE plugins or linters for the methodology yet?
**Answer:** The project is currently at the stage of finalizing the core specification (RFC). It is pointless to write tooling for rules that are still being polished. Basic tooling (plugins to enforce the `0,3,0` limit and validate the controlled dictionary) is already on the roadmap and will be released immediately following the stable 1.0 release.

---

🧬 **Quiql Ecosystem 2026** | Develop web with purpose.
