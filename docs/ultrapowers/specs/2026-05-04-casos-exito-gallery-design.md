# Design Spec: Galería de Casos de Éxito + Reemplazo de Imagen

**Date:** 2026-05-04  
**Project:** Sitio web Dra. Vannia Maldonado  
**Scope:** Agregar sección visual de casos de éxito y actualizar imagen de doctora

---

## Overview

Tres cambios coordenados para mejorar la conversión del sitio:
1. Reemplazar imagen de doctora con versión de mayor calidad
2. Agregar imágenes antes/después al slider existente
3. Crear sección nueva animada de casos de éxito (5 casos)

---

## 1. Reemplazar Imagen de Doctora

**Current State:**
- Imagen actual de la doctora en hero section: `vannia.jpg`

**Changes:**
- Reemplazar con: `WhatsApp Image 2026-05-02 at 19.45.17.jpeg`
- Ubicación: Mantener mismo DOM element (hero section)
- No cambios en estructura HTML/CSS
- Solo reemplazo de source del archivo

**Success Criteria:**
- Imagen carga correctamente en el hero
- Mantiene aspect ratio y responsive behavior

---

## 2. Slider Antes/Después

**Current State:**
- Slider existe con funcionalidad de desplazamiento implementada
- Ubicación: Section específica (verificar en HTML)

**Changes:**
- Agregar 2 nuevas imágenes del slider:
  - `WhatsApp Image 2026-05-02 at 19.58.11.jpeg`
  - `WhatsApp Image 2026-05-02 at 19.57.51 (1).jpeg`
- Integrar en carrusel existente
- Mantener funcionalidad actual de navegación

**Success Criteria:**
- Las nuevas imágenes se navegan con los controles del slider
- Mantiene animaciones/transiciones actuales

---

## 3. Nueva Sección: Galería de Casos de Éxito

### Structure

**Ubicación:** Justo después de `.services-section` (antes del footer/contacto)

**Contenido:**
- 5 casos de éxito (Caso 1 a Caso 5)
- Cada caso: 2 imágenes lado a lado (antes | después)
- Estructura de carpetas: `images/casos-exito/Caso 1/`, `Caso 2/`, etc.

### Layout

**Desktop:** 
- Grid 3 columnas (3 casos por fila)
- Cada tarjeta: 400px ancho x 300px alto aprox
- Espaciado: 24px entre items

**Tablet (768px):**
- Grid 2 columnas

**Mobile:**
- Stack vertical (1 columna)

### Animation

**Trigger:** Fade-in al scrollear (Intersection Observer)
- Opacidad: 0 → 1
- Duración: 600ms
- Easing: ease-out
- Delay por item: 100ms (efecto cascada)
- Z-index: Normal (se apilan naturalmente)

### Styling

**Card Container:**
- Background: `var(--bone)` (fondo del site)
- Border: 1px solid `var(--line)` (sutil)
- Border-radius: 8px
- Overflow: hidden

**Image Pair:**
- Flex row, dos imágenes iguales
- Cada imagen: 50% width
- Aspect ratio: 1:1 (square)
- Object-fit: cover (crop si es necesario)

**Hover State:**
- Subtle scale: 1.02x
- Transition: 300ms ease
- Box-shadow: 0 8px 24px rgba(0,0,0,0.08)

---

## 4. Implementation Notes

### File Organization

```
images/
├── casos-exito/
│   ├── Antes y después/
│   ├── Caso 1/
│   ├── Caso 2/
│   ├── Caso 3/
│   ├── Caso 4/
│   └── Caso 5/
```

### HTML Structure (Pseudo)

```html
<!-- After services section -->
<section class="success-cases">
  <h2>Casos de Éxito</h2>
  <div class="cases-grid">
    <div class="case-card" data-case="1">
      <div class="image-pair">
        <img src="..." alt="Antes - Caso 1">
        <img src="..." alt="Después - Caso 1">
      </div>
    </div>
    <!-- More cases... -->
  </div>
</section>
```

### CSS Implementation

- Fade animation via `opacity` with `transform: translateY(10px)` for subtle enter
- Intersection Observer for scroll-triggered animation
- Responsive grid with CSS Grid (not flexbox)

### Assets

- All images already in `images/casos-exito/`
- Total: 18 files (images + videos)
- Videos: Keep for potential future carousel feature

---

## Success Criteria

- [ ] Imagen de doctora actualizada con mejor calidad
- [ ] 2 nuevas imágenes en slider antes/después
- [ ] Sección casos-exito renderiza 5 casos en grid responsive
- [ ] Animación fade-in funciona al scrollear
- [ ] Hover effect sutil funciona en desktop
- [ ] Mobile responsive (1 columna en móvil)
- [ ] No hay layout shift o performance issues
- [ ] Imágenes cargadas optimizadas

---

## Out of Scope (Para después)

- Otros cambios estéticos mencionados por usuario
- Optimización de videos
- Lazy loading (si es necesario implementar después)
