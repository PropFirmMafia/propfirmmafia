# Prop Firm Mafia - Technical Specification

## Component Inventory

### shadcn/ui Components (Built-in)
| Component | Purpose | Customization |
|-----------|---------|---------------|
| Button | CTAs, navigation | Red accent variant, 3D hover |
| Card | Service cards, pricing, testimonials | Dark theme, glow effects |
| Accordion | FAQ section | 3D flip animation |
| Badge | "Popular" tag on pricing | Red glow pulse |
| Separator | Section dividers | Red accent line |

### Third-Party Registry Components
| Component | Registry | Purpose |
|-----------|----------|---------|
| @magicui/particles | magicui | Hero background particle effect |
| @magicui/number-ticker | magicui | Statistics counter animation |

### Custom Components
| Component | Purpose | Props |
|-----------|---------|-------|
| Navigation | Fixed nav with glassmorphism | - |
| Hero | Hero section with floating shards | - |
| ServiceCard | 3D service cards | title, description, price, features, icon |
| PricingCard | 3D pricing carousel cards | title, price, period, features, featured, cta |
| TestimonialCard | Masonry testimonial cards | quote, author, rating, service |
| StatCounter | Animated statistics | value, label, suffix |
| FAQAccordion | 3D accordion | items |
| CTASection | Diagonal CTA section | - |
| Footer | Site footer | - |

### Custom Hooks
| Hook | Purpose |
|------|---------|
| useScrollProgress | Track scroll position for animations |
| useInView | Intersection observer for triggering |
| useCountUp | Animated number counter |
| useMousePosition | Track mouse for magnetic effects |

---

## Animation Implementation Table

| Animation | Library | Implementation Approach | Complexity |
|-----------|---------|------------------------|------------|
| **Navigation glassmorphism** | CSS | backdrop-filter on scroll class | Low |
| **Nav link underline** | CSS | ::after pseudo-element width animation | Low |
| **Hero background zoom** | GSAP | ScrollTrigger scale/parallax | Medium |
| **Hero headline clip reveal** | GSAP | clip-path circle animation | High |
| **Hero floating shards** | CSS + GSAP | Keyframe animation + scroll scatter | Medium |
| **CTA 3D flip entrance** | GSAP | rotateX animation with opacity | Medium |
| **Service cards stack spread** | GSAP ScrollTrigger | Staggered translate/rotate on scroll | High |
| **Service card 3D hover** | CSS | transform with perspective | Low |
| **Pricing carousel 3D** | GSAP | rotateY + translateZ carousel | High |
| **Featured card glow pulse** | CSS | box-shadow keyframe animation | Low |
| **Statistics count up** | Custom hook | requestAnimationFrame counter | Medium |
| **Stat connection lines** | SVG + GSAP | stroke-dashoffset animation | Medium |
| **About image 3D tilt** | CSS | perspective + rotateY on hover | Low |
| **Testimonial card deal** | GSAP | Staggered rotate/translate entrance | Medium |
| **Testimonial card hover lift** | CSS | translateZ + z-index change | Low |
| **FAQ 3D accordion** | CSS + GSAP | rotateX unfold animation | Medium |
| **FAQ icon flip** | CSS | rotate transform | Low |
| **CTA gradient shift** | CSS | background-position animation | Low |
| **Button magnetic hover** | CSS | transform on :hover | Low |
| **Footer accent line** | GSAP | scaleX from center | Low |

---

## Animation Library Choices

### GSAP + ScrollTrigger
**Rationale:** Industry-standard for complex scroll animations, pinning, and timeline control.

**Used for:**
- Hero entrance sequence
- Service cards scroll spread
- Pricing carousel
- Statistics entrance
- Testimonial card deal animation

**Installation:**
```bash
npm install gsap @gsap/react
```

### CSS Animations
**Rationale:** Best performance for simple effects, no JS overhead.

**Used for:**
- Hover states
- Continuous ambient animations (glows, floats)
- Underline draws
- Gradient shifts

### Intersection Observer API
**Rationale:** Native API for triggering animations on viewport entry.

**Used for:**
- Section entrance triggers
- Counter animation start
- Lazy animation initialization

---

## Project File Structure

```
/mnt/okcomputer/output/app/
├── public/
│   ├── images/
│   │   ├── hero-bg.jpg
│   │   ├── about-image.jpg
│   │   └── favicon.ico
│   └── fonts/
├── src/
│   ├── components/
│   │   ├── ui/                    # shadcn components
│   │   │   ├── button.tsx
│   │   │   ├── card.tsx
│   │   │   ├── accordion.tsx
│   │   │   └── badge.tsx
│   │   ├── Navigation.tsx
│   │   ├── Hero.tsx
│   │   ├── Services.tsx
│   │   ├── ServiceCard.tsx
│   │   ├── Pricing.tsx
│   │   ├── PricingCard.tsx
│   │   ├── Statistics.tsx
│   │   ├── StatCounter.tsx
│   │   ├── About.tsx
│   │   ├── Testimonials.tsx
│   │   ├── TestimonialCard.tsx
│   │   ├── FAQ.tsx
│   │   ├── CTASection.tsx
│   │   └── Footer.tsx
│   ├── hooks/
│   │   ├── useScrollProgress.ts
│   │   ├── useInView.ts
│   │   └── useCountUp.ts
│   ├── lib/
│   │   └── utils.ts
│   ├── styles/
│   │   └── globals.css
│   ├── App.tsx
│   └── main.tsx
├── components.json
├── tailwind.config.js
├── tsconfig.json
└── package.json
```

---

## Dependencies

### Core
- react
- react-dom
- typescript
- vite

### UI
- tailwindcss
- @radix-ui/react-* (via shadcn)
- class-variance-authority
- clsx
- tailwind-merge
- lucide-react

### Animation
- gsap
- @gsap/react

### Fonts
- @fontsource/playfair-display
- @fontsource/inter
- @fontsource/cormorant-garamond

---

## CSS Custom Properties

```css
:root {
  /* Colors */
  --background: 0 0% 0%;
  --foreground: 0 0% 100%;
  --card: 0 0% 4%;
  --card-foreground: 0 0% 100%;
  --popover: 0 0% 4%;
  --popover-foreground: 0 0% 100%;
  --primary: 0 100% 50%;
  --primary-foreground: 0 0% 100%;
  --secondary: 0 0% 10%;
  --secondary-foreground: 0 0% 100%;
  --muted: 0 0% 15%;
  --muted-foreground: 0 0% 70%;
  --accent: 0 100% 50%;
  --accent-foreground: 0 0% 100%;
  --destructive: 0 84% 60%;
  --destructive-foreground: 0 0% 100%;
  --border: 0 0% 20%;
  --input: 0 0% 20%;
  --ring: 0 100% 50%;
  --radius: 0.5rem;

  /* Animation Easings */
  --ease-dramatic: cubic-bezier(0.87, 0, 0.13, 1);
  --ease-expo-out: cubic-bezier(0.16, 1, 0.3, 1);
  --ease-expo-in: cubic-bezier(0.7, 0, 0.84, 0);
  --ease-elastic: cubic-bezier(0.68, -0.55, 0.265, 1.55);
  --ease-smooth: cubic-bezier(0.4, 0, 0.2, 1);
  --ease-bounce: cubic-bezier(0.34, 1.56, 0.64, 1);
  --ease-liquid: cubic-bezier(0.23, 1, 0.32, 1);
}
```

---

## Tailwind Configuration Extensions

```javascript
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      fontFamily: {
        display: ['Playfair Display', 'serif'],
        sans: ['Inter', 'sans-serif'],
        accent: ['Cormorant Garamond', 'serif'],
      },
      colors: {
        background: 'hsl(var(--background))',
        foreground: 'hsl(var(--foreground))',
        card: 'hsl(var(--card))',
        'card-foreground': 'hsl(var(--card-foreground))',
        primary: 'hsl(var(--primary))',
        'primary-foreground': 'hsl(var(--primary-foreground))',
        secondary: 'hsl(var(--secondary))',
        'secondary-foreground': 'hsl(var(--secondary-foreground))',
        muted: 'hsl(var(--muted))',
        'muted-foreground': 'hsl(var(--muted-foreground))',
        accent: 'hsl(var(--accent))',
        'accent-foreground': 'hsl(var(--accent-foreground))',
        destructive: 'hsl(var(--destructive))',
        'destructive-foreground': 'hsl(var(--destructive-foreground))',
        border: 'hsl(var(--border))',
        input: 'hsl(var(--input))',
        ring: 'hsl(var(--ring))',
      },
      animation: {
        'float': 'float 4s ease-in-out infinite',
        'glow-pulse': 'glow-pulse 2s ease-in-out infinite',
        'gradient-shift': 'gradient-shift 8s ease infinite',
        'spin-slow': 'spin 20s linear infinite',
      },
      keyframes: {
        float: {
          '0%, 100%': { transform: 'translateY(0)' },
          '50%': { transform: 'translateY(-15px)' },
        },
        'glow-pulse': {
          '0%, 100%': { boxShadow: '0 0 20px rgba(255, 0, 0, 0.3)' },
          '50%': { boxShadow: '0 0 40px rgba(255, 0, 0, 0.5)' },
        },
        'gradient-shift': {
          '0%, 100%': { backgroundPosition: '0% 50%' },
          '50%': { backgroundPosition: '100% 50%' },
        },
      },
    },
  },
}
```

---

## Performance Optimization Strategy

### Animation Performance
1. **Use transform and opacity only** - GPU accelerated
2. **Apply will-change before animations** - Remove after completion
3. **Use CSS containment** - `contain: layout style paint`
4. **Throttle scroll events** - Use GSAP ScrollTrigger (optimized)
5. **Lazy load animations** - Trigger only when in viewport

### Image Optimization
1. **Use WebP format** where possible
2. **Implement lazy loading** - `loading="lazy"`
3. **Provide srcset** for responsive images
4. **Optimize file sizes** - Compress before adding to project

### Code Splitting
1. **Route-based splitting** - Each section as separate chunk
2. **Component lazy loading** - For below-fold content
3. **GSAP dynamic import** - Load only when needed

### Reduced Motion
```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}
```

---

## Build Configuration

### Vite Config
```javascript
// vite.config.ts
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'
import path from 'path'

export default defineConfig({
  plugins: [react()],
  resolve: {
    alias: {
      '@': path.resolve(__dirname, './src'),
    },
  },
  build: {
    target: 'esnext',
    minify: 'terser',
    cssMinify: true,
    rollupOptions: {
      output: {
        manualChunks: {
          'gsap-vendor': ['gsap', '@gsap/react'],
        },
      },
    },
  },
})
```

---

## Implementation Checklist

### Phase 1: Setup
- [ ] Initialize project with shadcn
- [ ] Install dependencies (GSAP, fonts)
- [ ] Configure Tailwind
- [ ] Set up folder structure

### Phase 2: Components
- [ ] Create shadcn components
- [ ] Build custom components
- [ ] Implement hooks

### Phase 3: Sections
- [ ] Navigation
- [ ] Hero
- [ ] Services
- [ ] Pricing
- [ ] Statistics
- [ ] About
- [ ] Testimonials
- [ ] FAQ
- [ ] CTA
- [ ] Footer

### Phase 4: Animation
- [ ] GSAP ScrollTrigger setup
- [ ] Entrance animations
- [ ] Scroll effects
- [ ] Hover interactions
- [ ] Continuous animations

### Phase 5: Polish
- [ ] Responsive testing
- [ ] Performance optimization
- [ ] Accessibility audit
- [ ] Cross-browser testing
