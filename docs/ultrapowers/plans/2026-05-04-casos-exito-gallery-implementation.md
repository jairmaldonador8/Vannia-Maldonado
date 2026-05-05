# Casos de Éxito Gallery Implementation Plan

> **For agentic workers:** Use ultrapowers:subagent-driven-development (recommended) or ultrapowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add a visually compelling cases gallery section with fade-in animations and replace the doctor's photo with higher quality version.

**Architecture:** Vanilla JavaScript (Intersection Observer) + CSS Grid responsive layout + GPU-accelerated animations. No dependencies. All changes in single HTML file with inline CSS/JS. Images organized in `images/casos-exito/` folder structure.

**Tech Stack:** 
- HTML5 semantic markup
- CSS Grid (auto-fit/minmax pattern)
- Intersection Observer API (native)
- CSS animations (opacity + transform GPU-accelerated)
- Native lazy loading (loading="lazy")

---

## File Structure

```
Vannia Maldonado/
├── index.html (MAIN - all changes here)
├── images/
│   ├── vannia.jpg (REPLACE - new high-quality photo)
│   └── casos-exito/ (NEW - all case images organized)
│       ├── Antes y después/
│       ├── Caso 1/
│       ├── Caso 2/
│       ├── Caso 3/
│       ├── Caso 4/
│       └── Caso 5/
```

---

## Implementation Tasks

### Task 1: Verify Image Assets Exist

**Files:**
- Check: `images/casos-exito/` folder structure
- Verify: All image paths exist

- [ ] **Step 1: Verify before/after slider images**

Check these paths exist:
```
images/casos-exito/Antes y después/WhatsApp Image 2026-05-02 at 19.57.51 (1).jpeg
images/casos-exito/Antes y después/WhatsApp Image 2026-05-02 at 19.58.11.jpeg
```

Expected: Both image files present, readable, ~500KB+ each (high quality).

- [ ] **Step 2: Verify success cases images**

Check all these paths exist:
```
images/casos-exito/Caso 1/WhatsApp Image 2026-05-02 at 19.52.50 (1).jpeg
images/casos-exito/Caso 2/WhatsApp Image 2026-05-02 at 19.53.17.jpeg
images/casos-exito/Caso 3/WhatsApp Image 2026-05-02 at 19.54.25.jpeg
images/casos-exito/Caso 4/WhatsApp Image 2026-05-02 at 19.56.14.jpeg
images/casos-exito/Caso 5/WhatsApp Image 2026-05-02 at 19.59.09.jpeg
images/casos-exito/Caso 5/WhatsApp Image 2026-05-02 at 19.59.09 (1).jpeg
```

Expected: All 6 image files present.

- [ ] **Step 3: Verify doctor image**

Check path exists:
```
c:\Users\bykai\OneDrive\Desktop\Vannia Maldonado fotos página\WhatsApp Image 2026-05-02 at 19.45.17.jpeg
```

Expected: File present, ~500KB+, high quality.

---

### Task 2: Prepare Doctor's Photo Asset

**Files:**
- Copy from: `c:\Users\bykai\OneDrive\Desktop\Vannia Maldonado fotos página\WhatsApp Image 2026-05-02 at 19.45.17.jpeg`
- Copy to: `Vannia Maldonado/vannia.jpg` (overwrite existing)

- [ ] **Step 1: Copy new doctor image to project root**

```bash
cp "c:\Users\bykai\OneDrive\Desktop\Vannia Maldonado fotos página\WhatsApp Image 2026-05-02 at 19.45.17.jpeg" "C:\Users\bykai\OneDrive\Documents\GitHub\Vannia Maldonado\vannia.jpg"
```

Expected: File copied successfully, ~500KB image file in project root.

- [ ] **Step 2: Verify image loads in browser**

Open in browser at: `file:///C:/Users/bykai/OneDrive/Documents/GitHub/Vannia%20Maldonado/index.html`

Expected: Doctor's photo in hero section displays with new high-quality image. No broken image icon.

---

### Task 3: Replace SVG Slider with Image-Based Before/After Slider

**Files:**
- Modify: `index.html` - replace entire `.before-after-section` content

**Current state:** Slider uses SVG illustrations. Replace with real before/after images with interactive drag effect.

- [ ] **Step 1: Find and replace SVG slider HTML**

**Search for:** `<section class="before-after-section" id="resultados">` (around line 3538)

**Replace the entire section (from `<section>` to `</section>`, lines ~3538-3615) with:**

```html
<!-- ============== ANTES/DESPUES SLIDER ============== -->
<section class="before-after-section" id="resultados">
  <div class="section-header reveal" style="margin: 0 auto 0; text-align: center;">
    <div class="section-eyebrow" style="justify-content: center;">Resultados visibles</div>
    <h2 class="section-title">Antes <span class="italic">y después.</span></h2>
    <p class="section-intro" style="margin: 0 auto;">Desliza para ver la transformación. Resultados sutiles, naturales y armónicos con tu rostro.</p>
  </div>

  <div class="before-after-container reveal-scale" id="baContainer">
    <!-- Before image (top layer) -->
    <div class="ba-image-wrapper ba-before-wrapper">
      <img 
        src="images/casos-exito/Antes y después/WhatsApp Image 2026-05-02 at 19.57.51 (1).jpeg" 
        alt="Antes de la cirugía" 
        class="ba-image ba-before"
        loading="eager"
        width="800"
        height="500"
      />
      <div class="ba-label before-label">Antes</div>
    </div>

    <!-- After image (bottom layer) -->
    <div class="ba-image-wrapper ba-after-wrapper">
      <img 
        src="images/casos-exito/Antes y después/WhatsApp Image 2026-05-02 at 19.58.11.jpeg" 
        alt="Después de la cirugía" 
        class="ba-image ba-after"
        loading="eager"
        width="800"
        height="500"
      />
      <div class="ba-label after-label">Después</div>
    </div>

    <!-- Draggable divider -->
    <div class="ba-divider" id="baDivider" style="left: 50%;"></div>
  </div>

  <p class="ba-instruction reveal">↔ Mueve el cursor o desliza para revelar el resultado</p>

  <p class="ba-disclaimer reveal" style="text-align: center; margin-top: 2rem; font-size: 0.9rem; color: #9C8A75; max-width: 600px; margin-left: auto; margin-right: auto; line-height: 1.6;">
    <em>Nota:</em> Los resultados mostrados son de pacientes reales con autorización. Cada paciente es único y los resultados varían según sus características anatómicas, tipo de piel y objetivos personales. Durante la consulta inicial, utilizamos simulación digital para visualizar el resultado esperado de forma personalizada.
  </p>
</section>
```

- [ ] **Step 2: Update CSS for image-based slider**

**Find in `<style>` tag:** `.ba-image` and `.ba-before`, `.ba-after` selectors

**Replace with:**

```css
/* Before-After Image Slider */
.before-after-container {
  position: relative;
  max-width: 800px;
  margin: 0 auto;
  overflow: hidden;
  border-radius: 8px;
  aspect-ratio: 16 / 10;
  cursor: col-resize;
  user-select: none;
}

.ba-image-wrapper {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
}

.ba-before-wrapper {
  z-index: 2;
}

.ba-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
}

.ba-divider {
  position: absolute;
  top: 0;
  width: 4px;
  height: 100%;
  background: var(--peach);
  cursor: col-resize;
  z-index: 5;
  box-shadow: 0 0 8px rgba(0,0,0,0.2);
  transition: box-shadow 0.2s ease;
}

.ba-divider:hover {
  box-shadow: 0 0 16px rgba(0,0,0,0.3);
}

.ba-divider::before {
  content: '';
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 40px;
  height: 40px;
  background: var(--peach);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.ba-divider::after {
  content: '◀ ▶';
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  color: var(--ink);
  font-size: 12px;
  font-weight: 600;
  letter-spacing: 2px;
  z-index: 1;
}

.ba-label {
  position: absolute;
  top: 16px;
  padding: 6px 12px;
  background: rgba(255,255,255,0.9);
  color: var(--ink);
  font-size: 0.75rem;
  font-weight: 600;
  letter-spacing: 1px;
  border-radius: 4px;
  z-index: 3;
  backdrop-filter: blur(4px);
}

.before-label {
  left: 16px;
}

.after-label {
  right: 16px;
}

@media (max-width: 768px) {
  .before-after-container {
    aspect-ratio: 4 / 3;
  }

  .ba-divider::before {
    width: 32px;
    height: 32px;
  }

  .ba-divider::after {
    font-size: 10px;
  }

  .ba-label {
    font-size: 0.7rem;
    padding: 4px 8px;
  }
}
```

- [ ] **Step 3: Add JavaScript for image slider interaction**

**Find in document:** Last `<script>` tag before `</body>` closing tag

**Add this new script before any existing IntersectionObserver code:**

```javascript
<!-- Before-After Image Slider Interaction -->
<script>
document.addEventListener('DOMContentLoaded', function() {
  const container = document.getElementById('baContainer');
  const divider = document.getElementById('baDivider');
  const beforeWrapper = document.querySelector('.ba-before-wrapper');
  let isActive = false;

  function updateDividerPosition(e) {
    if (!isActive && e.type !== 'touchstart' && e.type !== 'touchmove') return;
    
    const rect = container.getBoundingClientRect();
    let x = e.clientX - rect.left;
    
    // Handle touch events
    if (e.touches) {
      x = e.touches[0].clientX - rect.left;
    }
    
    // Clamp between 0 and container width
    x = Math.max(0, Math.min(x, rect.width));
    
    const percentage = (x / rect.width) * 100;
    
    divider.style.left = percentage + '%';
    beforeWrapper.style.clipPath = `inset(0 ${100 - percentage}% 0 0)`;
  }

  // Mouse events
  divider.addEventListener('mousedown', function() {
    isActive = true;
    container.style.cursor = 'col-resize';
  });

  document.addEventListener('mouseup', function() {
    isActive = false;
  });

  document.addEventListener('mousemove', function(e) {
    if (isActive) {
      updateDividerPosition(e);
    }
  });

  // Hover effect on container
  container.addEventListener('mousemove', function(e) {
    if (!isActive) {
      updateDividerPosition(e);
    }
  });

  // Touch events for mobile
  let touchStartX = 0;
  container.addEventListener('touchstart', function(e) {
    touchStartX = e.touches[0].clientX;
    isActive = true;
  });

  container.addEventListener('touchend', function() {
    isActive = false;
  });

  container.addEventListener('touchmove', function(e) {
    // Only update if touch actually moved (prevents phantom updates)
    const touchCurrentX = e.touches[0].clientX;
    if (Math.abs(touchCurrentX - touchStartX) > 2) {
      updateDividerPosition(e);
      touchStartX = touchCurrentX;
    }
  });

  // Initialize divider at 50%
  divider.style.left = '50%';
  beforeWrapper.style.clipPath = 'inset(0 50% 0 0)';
});
</script>
```

- [ ] **Step 4: Test slider in browser**

Open in browser, scroll to "Resultados" section.

Expected:
- Two real before/after images visible
- Dragging divider left/right updates clip-path
- Hovering over image updates divider position (smooth reveal)
- Mobile: touch and drag works smoothly
- Labels "Antes" and "Después" visible in corners
- No SVG elements visible (completely replaced)

---

### Task 4: Add CSS for Cases Gallery Section

**Files:**
- Modify: `index.html` - add styles to `<style>` tag (before closing `</style>`)

**Insert after existing service card styles:**

```css
/* ===== CASOS DE ÉXITO GALLERY ===== */
.success-cases {
  padding: 4rem 2rem;
  background: var(--bone);
}

.success-cases-container {
  max-width: 1200px;
  margin: 0 auto;
}

.success-cases-title {
  font-family: 'Fraunces', serif;
  font-size: clamp(1.8rem, 4vw, 3rem);
  font-weight: 300;
  color: var(--ink);
  margin-bottom: 3rem;
  text-align: center;
}

.cases-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
  gap: 24px;
  margin-bottom: 2rem;
}

.case-card {
  background: var(--cream-light);
  border: 1px solid var(--line);
  border-radius: 8px;
  overflow: hidden;
  opacity: 0;
  transform: translateY(10px);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.case-card.visible {
  animation: fadeInGallery 0.6s cubic-bezier(0.25, 0.46, 0.45, 0.94) forwards;
  animation-delay: var(--stagger-delay, 0ms);
}

.case-card:hover {
  transform: scale(1.02);
  box-shadow: 0 8px 24px rgba(110, 93, 67, 0.12);
}

.case-card img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
}

.image-pair {
  display: flex;
  width: 100%;
  height: 100%;
}

.image-pair img {
  width: 50%;
  height: 100%;
  object-fit: cover;
  border-right: 2px solid var(--line);
}

.image-pair img:last-child {
  border-right: none;
}

@keyframes fadeInGallery {
  from {
    opacity: 0;
    transform: translateY(10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Responsive adjustments */
@media (max-width: 768px) {
  .success-cases {
    padding: 3rem 1.5rem;
  }

  .cases-grid {
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 16px;
  }

  .image-pair {
    height: 250px;
  }

  .case-card:hover {
    transform: scale(1.01);
  }
}

@media (max-width: 480px) {
  .cases-grid {
    grid-template-columns: 1fr;
    gap: 12px;
  }

  .image-pair {
    height: 200px;
  }

  .success-cases-title {
    font-size: 1.4rem;
  }
}
```

- [ ] **Step 1: Open index.html in editor**

- [ ] **Step 2: Find closing `</style>` tag**

Search for the last `</style>` in the document (should be near line ~2800 based on file size).

- [ ] **Step 3: Insert gallery CSS before `</style>`**

Paste the CSS block above before closing tag.

- [ ] **Step 4: Verify CSS loads (check browser DevTools)**

Expected: New `.success-cases`, `.cases-grid`, `.case-card` styles visible in DevTools.

---

### Task 5: Add HTML Structure for Cases Gallery Section

**Files:**
- Modify: `index.html` - insert new section after `.services-horizontal` closes

**Location:** Find the line with `</section>` that closes `.services-horizontal`, and insert the new section RIGHT AFTER IT (before the `.stats` section).

**Insert this HTML block:**

```html
<!-- CASOS DE ÉXITO SECTION -->
<section class="success-cases">
  <div class="success-cases-container">
    <h2 class="success-cases-title">Casos de <span class="italic">Éxito.</span></h2>
    
    <div class="cases-grid">
      <!-- Case 1 -->
      <div class="case-card" data-case="1">
        <img src="images/casos-exito/Caso 1/WhatsApp Image 2026-05-02 at 19.52.50 (1).jpeg" 
             alt="Caso de éxito 1" 
             loading="lazy"
             width="400" height="300" />
      </div>

      <!-- Case 2 -->
      <div class="case-card" data-case="2">
        <img src="images/casos-exito/Caso 2/WhatsApp Image 2026-05-02 at 19.53.17.jpeg" 
             alt="Caso de éxito 2" 
             loading="lazy"
             width="400" height="300" />
      </div>

      <!-- Case 3 -->
      <div class="case-card" data-case="3">
        <img src="images/casos-exito/Caso 3/WhatsApp Image 2026-05-02 at 19.54.25.jpeg" 
             alt="Caso de éxito 3" 
             loading="lazy"
             width="400" height="300" />
      </div>

      <!-- Case 4 -->
      <div class="case-card" data-case="4">
        <img src="images/casos-exito/Caso 4/WhatsApp Image 2026-05-02 at 19.56.14.jpeg" 
             alt="Caso de éxito 4" 
             loading="lazy"
             width="400" height="300" />
      </div>

      <!-- Case 5 (has 2 images for before/after) -->
      <div class="case-card" data-case="5">
        <div class="image-pair">
          <img src="images/casos-exito/Caso 5/WhatsApp Image 2026-05-02 at 19.59.09.jpeg" 
               alt="Caso 5 - Antes" 
               loading="lazy"
               width="200" height="300" />
          <img src="images/casos-exito/Caso 5/WhatsApp Image 2026-05-02 at 19.59.09 (1).jpeg" 
               alt="Caso 5 - Después" 
               loading="lazy"
               width="200" height="300" />
        </div>
      </div>
    </div>
  </div>
</section>
```

- [ ] **Step 1: Find closing `</section>` of `.services-horizontal`**

Search for: `id="servicios"` → scroll down to find where that section closes with `</section>`

Expected: Find it around line 3330-3340 area.

- [ ] **Step 2: Insert new cases gallery section**

Add the HTML block right after the services section closes, BEFORE the `.stats` section begins.

- [ ] **Step 3: Verify HTML structure in browser**

Open in browser, scroll down past services section.

Expected: "Casos de Éxito" heading visible but images show placeholder/loading state (fade-in animation hasn't triggered yet — that's Step 5).

---

### Task 6: Add JavaScript for Intersection Observer (Scroll Animations)

**Files:**
- Modify: `index.html` - add JavaScript at end of document (before closing `</body>`)

**Insert this JavaScript block before `</body>` closing tag:**

```javascript
<!-- Intersection Observer for Gallery Fade-In -->
<script>
document.addEventListener('DOMContentLoaded', function() {
  const observerOptions = {
    threshold: 0.1,
    rootMargin: '0px 0px -50px 0px'
  };

  const observer = new IntersectionObserver(function(entries) {
    entries.forEach(function(entry) {
      if (entry.isIntersecting) {
        // Calculate stagger delay based on position in grid
        const cards = Array.from(document.querySelectorAll('.case-card'));
        const cardIndex = cards.indexOf(entry.target);
        
        // Set CSS custom property for animation delay (CSS handles animation)
        entry.target.style.setProperty('--stagger-delay', (cardIndex * 100) + 'ms');
        
        // Add visible class to trigger CSS animation
        entry.target.classList.add('visible');
        
        // Stop observing this element after triggering
        observer.unobserve(entry.target);
      }
    });
  }, observerOptions);

  // Observe all case cards
  document.querySelectorAll('.case-card').forEach(function(card) {
    observer.observe(card);
  });
});
</script>
```

- [ ] **Step 1: Open index.html at the end**

Scroll to very bottom, find `</body>` closing tag.

- [ ] **Step 2: Insert JavaScript block before `</body>`**

Paste the entire `<script>` block above.

- [ ] **Step 3: Test animations in browser**

Open in browser, scroll down to cases section slowly.

Expected: As you scroll, each case card fades in one by one (100ms stagger between cards). Hover on desktop shows subtle scale effect.

---

### Task 7: Verify Image Assets Load Correctly

**Files:**
- Check: `images/casos-exito/` folder structure
- Verify: All image paths match HTML `src` attributes

- [ ] **Step 1: Check images folder contents**

Verify all these paths exist:
```
images/casos-exito/Caso 1/WhatsApp Image 2026-05-02 at 19.52.50 (1).jpeg
images/casos-exito/Caso 2/WhatsApp Image 2026-05-02 at 19.53.17.jpeg
images/casos-exito/Caso 3/WhatsApp Image 2026-05-02 at 19.54.25.jpeg
images/casos-exito/Caso 4/WhatsApp Image 2026-05-02 at 19.56.14.jpeg
images/casos-exito/Caso 5/WhatsApp Image 2026-05-02 at 19.59.09.jpeg
images/casos-exito/Caso 5/WhatsApp Image 2026-05-02 at 19.59.09 (1).jpeg
```

- [ ] **Step 2: Browser DevTools - Network tab**

Open DevTools → Network tab → Reload page → Scroll to cases section.

Expected: All case images load successfully (200 status), no 404 errors. Images load on-demand (lazy loading).

- [ ] **Step 3: Check for broken images**

Scroll through cases section visually.

Expected: All before/after image pairs display correctly, no broken/missing image icons.

---

### Task 8: Test Responsive Design (Mobile/Tablet)

**Files:**
- Test: `index.html` in responsive mode

- [ ] **Step 1: Open DevTools Responsive Design Mode**

In browser: F12 → click device toolbar → test these breakpoints:
- Desktop (1200px+)
- Tablet (768px)
- Mobile (480px)

- [ ] **Step 2: Test on Desktop (1200px+)**

Expected: 3 columns of cases, images 300x300px, hover scale works.

- [ ] **Step 3: Test on Tablet (768px)**

Expected: 2 columns of cases, images 250x250px, grid adjusts gracefully.

- [ ] **Step 4: Test on Mobile (480px)**

Expected: 1 column (full width), images 200x200px, stacks vertically, fade-in animations work.

- [ ] **Step 5: Test scroll animation on mobile**

Expected: Fade-in animations trigger smoothly as you scroll on mobile (60 FPS, no jank).

---

### Task 9: Final Cross-Browser Testing

**Files:**
- Test: `index.html` in multiple browsers

- [ ] **Step 1: Test in Chrome/Chromium**

Expected: All animations smooth, lazy loading works, grid responsive.

- [ ] **Step 2: Test in Firefox**

Expected: Same behavior as Chrome.

- [ ] **Step 3: Test in Safari (if available)**

Expected: GPU acceleration, animations smooth, no webkit-specific issues.

- [ ] **Step 4: Check image quality**

Expected: Doctor photo in hero displays at high quality, no compression artifacts. Before/after cases show clear visual comparison.

---

### Task 10: Commit Changes (If Auto-Commit Enabled)

**Condition:** Only if `autoCommit: true` in `.claude/ultrapowers-preferences.json`

- [ ] **Step 1: Stage all changes**

```bash
git add index.html vannia.jpg docs/
```

- [ ] **Step 2: Commit with clear message**

```bash
git commit -m "feat: add success cases gallery with fade-in animations and new doctor photo

- Replace doctor photo with high-quality version
- Add 2 new before/after images to slider
- Create new cases gallery section after services
- Implement CSS Grid responsive layout (3/2/1 columns)
- Add Intersection Observer fade-in animations with cascade delays
- Use native lazy loading for image optimization
- GPU-accelerated animations (opacity + transform)

All images organized in images/casos-exito/ folder"
```

Expected: Clean commit with all changes staged.

- [ ] **Step 3: Push to remote (If Auto-Push Enabled)**

```bash
git push origin main
```

Expected: Changes pushed to GitHub successfully.

---

## Success Criteria Checklist

- [ ] Doctor's photo replaced with high-quality version
- [ ] 2 new before/after images added to slider
- [ ] Cases gallery section displays 5 success cases
- [ ] Fade-in animations trigger on scroll with cascade effect
- [ ] CSS Grid responsive: 3 columns (desktop), 2 (tablet), 1 (mobile)
- [ ] All images lazy-load (`loading="lazy"` working)
- [ ] Hover effects work smoothly on desktop
- [ ] No layout shift as images load (width/height specified)
- [ ] Cross-browser tested (Chrome, Firefox, Safari)
- [ ] No console errors in DevTools
- [ ] Performance: animations at 60 FPS (no jank)
- [ ] Git commits clean and descriptive (if auto-commit enabled)

---

## Notes for Implementation

**Reference Documents:**
- Spec: `docs/ultrapowers/specs/2026-05-04-casos-exito-gallery-design.md`
- Research: `docs/ultrapowers/research/2026-05-04-gallery-animations-research.md`

**Key Patterns Used:**
1. **Intersection Observer + CSS** — Most performant for scroll animations
2. **CSS Grid auto-fit** — Automatically responsive without media queries
3. **Native lazy loading** — No JS overhead
4. **GPU-accelerated animations** — opacity + transform (no width/height)
5. **Cascade delays** — CSS custom properties (`--stagger-delay`)

**Common Pitfalls to Avoid:**
- ❌ Don't animate width/height (use transform instead)
- ❌ Don't forget `unobserve()` in IntersectionObserver callback (memory leak)
- ❌ Don't remove `width`/`height` from images (layout shift)
- ❌ Don't use `scroll` event listener (use IntersectionObserver)
- ✅ Do test animations on actual mobile (DevTools can be misleading)
