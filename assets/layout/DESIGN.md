# Design System Document: High-End Real Estate Editorial

## 1. Overview & Creative North Star

**Creative North Star: "The Architectural Monograph"**

This design system moves beyond the standard real estate portal to create a digital experience that feels like a premium architectural monograph. The goal is to mirror the physical characteristics of the 'Dom w Cyklamenach'—the interplay of light on off-white plaster, the solid charcoal of the roof, and the surprising, vibrant bloom of the cyclamen flower.

We break the "template" look through **Intentional Asymmetry**. Instead of centered, predictable grids, we utilize the spacing scale to create wide, luxurious gutters and overlapping elements where images bleed off-screen or sit partially behind text containers. This creates a sense of depth and curated "editorial" pacing, making the user feel they are browsing a high-end lifestyle magazine rather than a listing database.

---

## 2. Colors

The palette is rooted in the structural tones of the house facade, accented by a singular, high-fashion floral pop.

### Color Tokens
*   **Primary (Cyclamen):** `#a9216d` – Used exclusively for high-impact CTAs and key brand moments.
*   **Surface Hierarchy:**
    *   `background`: `#f8fafb` (The main "canvas")
    *   `surface-container-low`: `#f2f4f5` (Subtle section shifts)
    *   `surface-container-highest`: `#e1e3e4` (Deeply nested elements)
    *   `surface-container-lowest`: `#ffffff` (Pure white cards for maximum lift)
*   **Neutrals:** `secondary` (`#575f69`) and `outline` (`#88717a`) provide the architectural grey weight.

### Strategic Application
*   **The "No-Line" Rule:** We do not use 1px solid lines to separate the kitchen from the living room; we do not use them in UI either. Boundaries must be defined solely by shifting from `surface` to `surface-container-low`.
*   **Glass & Gradient Rule:** To add "soul," CTAs should not be flat. Use a subtle linear gradient from `primary` (#a9216d) to `primary_container` (#c93d87) at a 135-degree angle. Floating navigation or image captions should use **Glassmorphism**: `surface` at 70% opacity with a `24px` backdrop-blur.
*   **Signature Textures:** Use the `primary_fixed_dim` (#ffb0d0) at 5% opacity as a large, decorative background element (like a faded flower motif or large-scale serif numeral) to break up large white spaces.

---

## 3. Typography

The typography strategy pairs the structural precision of **Manrope** with the approachable modernism of **Plus Jakarta Sans**.

*   **Display (Manrope):** Large-scale, low-tracking (letter-spacing: -0.02em). This represents the "bones" of the house.
    *   `display-lg`: 3.5rem. Use for hero titles.
*   **Headlines (Manrope):** Bold and authoritative.
    *   `headline-md`: 1.75rem. Use for section titles like "Interior Gallery."
*   **Body (Plus Jakarta Sans):** Chosen for its high x-height and readability.
    *   `body-lg`: 1rem. Used for property descriptions.
*   **Labels (Plus Jakarta Sans):** All-caps with increased tracking (+0.05em) for a technical, "blueprint" feel.
    *   `label-md`: 0.75rem. Used for specs (e.g., "SQUARE FOOTAGE").

---

## 4. Elevation & Depth

We convey luxury through **Tonal Layering** rather than traditional drop shadows.

*   **The Layering Principle:** A property feature card (`surface-container-lowest`) should sit atop a `surface-container-low` section. This provides a soft, natural lift that mimics architectural planes.
*   **Ambient Shadows:** If a floating element (like a "Book a Tour" fab) requires a shadow, it must use a `24px` blur at 6% opacity, using the `on-surface` (#191c1d) color. This creates an "atmospheric" rather than "heavy" feel.
*   **The "Ghost Border" Fallback:** For input fields or secondary buttons, use the `outline-variant` (#dbbfc9) at **20% opacity**. It should be felt, not seen.
*   **Roundedness:** We use a refined **md (0.375rem)** for functional components and **xl (0.75rem)** for large imagery, echoing the clean but softened edges of modern residential design.

---

## 5. Components

### Buttons
*   **Primary:** Gradient `primary` to `primary_container`. White text. `xl` roundedness. 
*   **Secondary:** No background. `Ghost Border` (20% opacity `outline-variant`). `secondary` text.
*   **Tertiary:** Text-only in `primary` color with a `2px` underline that appears on hover.

### Cards & Lists
*   **Forbid dividers.** Use `Spacing 8` (2.75rem) to separate property features. 
*   **Interactive Cards:** On hover, a card should shift from `surface-container-low` to `surface-container-lowest` and gain a subtle Ambient Shadow.

### Input Fields
*   **Styling:** Minimalist. Only a bottom border of `outline-variant` at 40%. On focus, the border becomes `primary` and grows to 2px.

### Architectural Breadcrumbs
*   A custom component for real estate: A thin vertical line (using `primary` at 30% opacity) that tracks the user's scroll progress through different floors or sections of the house.

---

## 6. Do's and Don'ts

### Do:
*   **Embrace the Void:** Use `Spacing 20` (7rem) and `Spacing 24` (8.5rem) to create dramatic pauses between sections.
*   **Layer Imagery:** Let a high-res photo of the house exterior overlap with a `surface-container-lowest` text block by `Spacing 10` (3.5rem).
*   **Use Tonal Shifts:** Define the footer by moving from `surface` to `surface-dim`.

### Don't:
*   **Don't use black:** Use `on-surface` (#191c1d) for text. Pure black is too harsh for the "fresh" atmosphere.
*   **Don't use standard icons:** Use thin-stroke (1px or 1.5px) icons that match the `secondary` or `primary` color.
*   **Don't center everything:** High-end design thrives on an asymmetrical balance. If an image is on the left, let the text sit high-right, not perfectly centered.
*   **No "Boxy" Containers:** Avoid wrapping everything in a bordered box. Let the content breathe against the background.