# Design System Strategy: The Technical Editorial

## 1. Overview & Creative North Star: "The Digital Curator"
This design system moves beyond the standard documentation template to create a high-end, editorial experience for technical content. Our Creative North Star is **"The Digital Curator."** 

Unlike generic documentation that feels like a dense manual, this system treats technical information as a curated exhibition. We achieve this through a "Macro-to-Micro" layout strategy: using expansive white space and intentional asymmetry to draw the eye, while maintaining a rigid, mathematical precision in the details. By breaking the standard full-width grid and using "offset" content blocks, we signal to the user that this experience is bespoke, authoritative, and premium.

---

## 2. Colors & Surface Architecture
The palette is rooted in a sophisticated monochrome spectrum, punctuated by a surgical use of `primary` (#0058bc) for intent and action.

### The "No-Line" Rule
Standard 1px solid borders are strictly prohibited for sectioning. Structural boundaries must be defined solely through background color shifts. For example, a sidebar using `surface_container_low` (#f3f3f5) should sit directly against a `surface` (#f9f9fb) main content area. The transition of tone is the divider.

### Surface Hierarchy & Nesting
Treat the UI as a series of physical layers—like stacked sheets of fine vellum.
*   **Base:** `background` (#f9f9fb)
*   **Secondary Content Areas:** `surface_container` (#eeeef0)
*   **Floating Elements/Cards:** `surface_container_lowest` (#ffffff)
*   **High-Emphasis Interaction:** `surface_container_high` (#e8e8ea)

### The "Glass & Gradient" Rule
To avoid a "flat" or "bootstrap" appearance, use Glassmorphism for floating navigation bars or contextual menus. Apply `surface_container_lowest` at 80% opacity with a `backdrop-blur` of 20px. 

### Signature Textures
Main CTAs should not be flat. Use a subtle linear gradient from `primary` (#0058bc) to `primary_container` (#0070eb) at a 135-degree angle. This adds a "lithographic" depth that flat hex codes cannot replicate.

---

## 3. Typography: The Authority of Scale
We utilize a technical-editorial typographic scale. While the typeface (Inter/SF Pro style) is utilitarian, the application is dramatic.

*   **Display Scale (`display-lg` to `display-sm`):** Reserved for high-level landing pages. Use `display-md` (2.75rem) with a tight tracking (-0.02em) to create a "Technical Vogue" feel.
*   **Headline & Title:** Use `headline-sm` (1.5rem) for section headers. Ensure a generous `6` (1.5rem) spacing units below headers to allow the typography to breathe.
*   **Body & Label:** Use `body-md` (0.875rem) for primary documentation. For technical metadata, use `label-md` (0.75rem) in `secondary` (#5f5e5e) to create a clear functional hierarchy.

---

## 4. Elevation & Depth: Tonal Layering
Traditional drop shadows are too "heavy" for a minimalist technical system. We convey depth through light and tone.

*   **The Layering Principle:** Instead of a shadow, place a `surface_container_lowest` card on a `surface_container_low` section. The slight shift from #ffffff to #f3f3f5 creates a "soft lift" that feels architectural rather than digital.
*   **Ambient Shadows:** If a floating element (like a modal) requires a shadow, use a "Cloud Shadow": `box-shadow: 0 12px 40px rgba(0, 88, 188, 0.04);`. Note the use of a `primary` tint in the shadow to make it feel integrated into the lighting of the page.
*   **The "Ghost Border" Fallback:** If a border is required for accessibility (e.g., in a high-contrast state), use `outline_variant` (#c1c6d7) at 20% opacity. 100% opaque borders are forbidden.

---

## 5. Components

### Buttons
*   **Primary:** Gradient fill (`primary` to `primary_container`), `xl` (0.75rem) roundedness, and `on_primary` text.
*   **Secondary:** `surface_container_highest` (#e2e2e4) background with `primary` text. No border.
*   **Tertiary:** Ghost style. `on_surface` text with no background. On hover, transition to `surface_container_low`.

### Input Fields
Avoid the "box" look. Use a `surface_container_lowest` background with a `2px` bottom-only border in `outline_variant` at 40% opacity. Upon focus, the bottom border scales to 100% opacity `primary`.

### Cards & Lists
*   **Rule:** Forbid the use of divider lines. 
*   **Alternative:** Use vertical white space (`4` to `6` on the scale) to separate items. For lists, use a hover state that changes the background to `surface_container_low` with a `md` (0.375rem) corner radius to highlight the active row.

### The "Breadcrumb Navigator"
A custom component for this system. Use `label-sm` typography in all-caps with 0.1em letter spacing. Separate items with a `primary` colored dot (3px) rather than a slash.

---

## 6. Do's and Don'ts

### Do
*   **Do** use asymmetrical margins. If the main content is 800px wide, offset it to the left to leave a wide right-hand margin for "Curator Notes" (annotations).
*   **Do** use `primary` (#0058bc) exclusively for interactive elements. If it’s blue, it must be clickable.
*   **Do** leverage the `0.5` (0.125rem) spacing unit for micro-alignments in icons and labels.

### Don't
*   **Don't** use pure black (#000000) for body text. Use `on_surface` (#1a1c1d) to maintain a premium, ink-on-paper feel.
*   **Don't** use standard "Drop Shadows." If it looks like a default Photoshop shadow, it is wrong. Use Tonal Layering.
*   **Don't** use "Dividers" to separate sections. Use a `2.5rem` (`10`) vertical gap or a background color shift.