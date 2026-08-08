# Lead.AI Phase 1 — Design System & Theme Specification
**Last Verified:** 2026-08-08  

---

## 1. THEME ARCHITECTURE

- **Provider:** `next-themes` (`ThemeProvider` wrapped at top level in `App.tsx`)
- **Strategy:** Class-based Tailwind dark mode (`attribute="class"`, `defaultTheme="system"`)
- **Persistence:** LocalStorage key `theme` with initial hydration flash prevention.

---

## 2. COLOR PALETTE & CSS TOKENS

### Light Mode (`:root`)
- Background: `hsl(210 40% 98%)` (Calm Slate Soft White)
- Foreground: `hsl(215 28% 17%)` (Deep Slate Neutral)
- Cards & Surfaces: `hsl(0 0% 100%)` with soft elevation `0 4px 24px hsl(215 28% 17% / 0.08)`
- Primary Accent: `hsl(221 83% 53%)` (Electric Sapphire)
- Secondary Accent: `hsl(189 94% 43%)` (Cyan Blue)

### Dark Mode (`.dark`)
- Background: `hsl(222 47% 11%)` (Deep Midnight Navy)
- Foreground: `hsl(210 40% 98%)` (High Contrast Soft White)
- Cards & Surfaces: `hsl(222 47% 13%)` with subtle borders `hsl(217 33% 20%)`
- Elevated Glass Panels: `hsl(222 47% 11% / 0.7)` with `backdrop-filter: blur(12px)`

---

## 3. ACCESSIBILITY & CONTRAST

- Contrast ratio exceeds WCAG AA standards in both light and dark themes.
- Accessible ARIA labels on theme toggle controls (`aria-label="Change color theme"`).
- Keyboard focus rings visible (`ring-2 ring-primary`).
