# Design System & Architecture

## Color Palette

### Primary Colors (Cyberpunk Theme)
- **Cyan**: `#22D3EE` - Primary accent, links, active states
- **Purple**: `#8B5CF6` - Secondary accent, backgrounds, borders
- **Pink**: `#EC4899` - Tertiary accent, highlights, warnings
- **Teal**: `#14B8A6` - Quaternary accent, alternative highlights
- **Sky Blue**: `#38BDF8` - Supporting text, secondary elements

### Neutral Colors
- **Dark Background**: `#050816` - Primary background
- **Dark Overlay**: `#070C1E` - Secondary background
- **Dark Accent**: `#0F172A` - Tertiary background
- **Light Text**: `#F8FAFC` - Primary text (headings)
- **Medium Text**: `#CBD5E1` - Secondary text
- **Dim Text**: `#94A3B8` - Tertiary text
- **Gray Text**: `#64748B` - Quaternary text

## Typography

### Font Families
- **Display/Headings**: `'Inter', system-ui, -apple-system, sans-serif`
  - Font weights: 700 (bold), 800 (extra-bold)
  - Letter spacing: -0.02em for headlines
  - Font size: 54px for main heading

- **Code/Terminal**: `'Fira Code', monospace`
  - Font weights: 600 (semibold), 700 (bold)
  - Font sizes: 12px-16px
  - Used for: badges, terminal-style text, stats

- **Body**: `system-ui, -apple-system, sans-serif`
  - Font weights: 400 (normal), 500 (medium)
  - Font sizes: 12px-18px
  - Used for: descriptions, table content

### Text Colors
| Element | Color | Hex |
|---------|-------|-----|
| Main Heading | Light | #F8FAFC |
| Section Heading | Cyan | #22D3EE |
| Body Text | Medium | #CBD5E1 |
| Secondary Text | Dim | #94A3B8 |
| Terminal Text | Cyan | #22D3EE |
| Command Prompt | Purple | #8B5CF6 |
| Links | Cyan | #22D3EE (hover: brighter) |
| Badges | Varied by tech stack | (See tech stack section) |

## Visual Elements

### Cards & Panels
- Border radius: 12-14px
- Border width: 1-1.5px
- Border colors: Cyan (0.3-0.45 opacity) or Pink (0.4 opacity)
- Background: Gradient from dark to darker (see gradients below)
- Shadow: Glow filter with 5-8px blur

### Gradients
#### Background Gradient
```
From: #02040A (top-left)
Via: #070C1E (middle)
To: #0F172A (bottom-right)
```

#### Neon Gradient
```
0%: #14B8A6 (teal)
30%: #22D3EE (cyan)
65%: #8B5CF6 (purple)
100%: #EC4899 (pink)
```

#### Card Gradient 1 (Left Panel)
```
0%: #090D1F (opacity 0.85)
100%: #030712 (opacity 0.95)
```

#### Card Gradient 2 (Right Panel)
```
0%: #0B0F29 (opacity 0.85)
100%: #030712 (opacity 0.95)
```

## Animations

### Duration Standards
- Quick feedback: 200ms
- Smooth transitions: 400-500ms
- Pulse/breathing: 2-3s
- Wave/flow: 4-8s
- Entrance: 0.6-0.8s

### Animation Types
| Animation | Duration | Easing | Use Case |
|-----------|----------|--------|----------|
| `glow-pulse` | 3s | ease-in-out | Grid, card backgrounds |
| `slide-right` | 0.8s | ease-out | Card entrance, panel load |
| `float-up` | 2.5s | ease-in-out | Floating elements, dialog boxes |
| `neon-glow` | 2s | ease-in-out | Wave paths, accent lines |
| `pulse-glow` | 4s | ease-in-out | Footer grid, subtle pulses |
| `wave-flow` | 8s | linear | SVG path animations |
| `text-glow` | 3s | ease-in-out | Glowing text, headers |
| `blink` | 1s | steps(1) | Cursor, indicators |
| `typewriter` | 4s | steps(60) | Typing effect |

### Accessibility
- All animations respect `prefers-reduced-motion` media query
- Animations use `ease-in-out` for smooth, predictable motion
- No animations exceed 10 seconds
- Blinking elements have clear purpose and off-period

## Responsive Design

### Breakpoints
| Device | Viewport | Adjustments |
|--------|----------|-------------|
| Mobile | 320px | Single column, stacked layout |
| Tablet | 768px | Two-column where applicable |
| Desktop | 1024px+ | Full layout with sidebars |
| Large | 1440px+ | Optimized spacing |

### Responsive Behaviors
- SVG images: `width="100%"` for fluid scaling
- Images: `loading="lazy"` for performance
- Tables: Stack on mobile, side-by-side on desktop
- Badges: Wrap with `flex-wrap: wrap`
- Font sizes: Scale from 12px (mobile) to 18px+ (desktop)
- Touch targets: Minimum 44x44px on mobile

## SVG Assets

### Hero SVG (profile-hero.svg)
- **Dimensions**: 1200x390px (responsive via `width="100%"`)
- **Content**: Terminal panels, wave path, hero typography
- **Animations**: 
  - Grid pulse (subtle background)
  - Card slide entrance
  - Wave glow
  - Float animation for right panel
- **Performance**: Optimized with SVG filters, ~8KB

### Footer SVG (profile-footer.svg)
- **Dimensions**: 1200x180px (responsive via `width="100%"`)
- **Content**: Status indicator, wave path, footer text
- **Animations**:
  - Grid pulse
  - Wave flow
  - Text glow
  - Indicator pulse (animated circle)
- **Performance**: Optimized, ~6KB

### Fallback Stats SVGs
| File | Size | Purpose |
|------|------|---------|
| `stats-fallback-github.svg` | 400x150 | GitHub stats backup |
| `stats-fallback-languages.svg` | 400x150 | Language breakdown |
| `stats-fallback-streak.svg` | 400x150 | Contribution streak |
| `contribution-grid-static.svg` | 1200x200 | Activity grid fallback |
| `profile-typing-static.svg` | 900x60 | Static typing display |
| `profile-typing.svg` | 900x60 | Animated typing display |

## Performance Optimization

### Load Strategy
1. **Critical**: Hero and footer SVGs (inline or cached)
2. **High Priority**: GitHub badge images (served from img.shields.io)
3. **Fallback**: Local SVG alternatives (loaded if external fails)
4. **Low Priority**: Contribution grid (lazy loaded if external)

### Image Loading
```html
<!-- Progressive enhancement -->
<picture>
  <source media="(prefers-reduced-motion: no-preference)" 
          srcset="./assets/animated.svg">
  <img src="./assets/static.svg" alt="..." />
</picture>
```

### Optimization Techniques
- SVG filters use efficient Gaussian blur
- CSS animations prefer transform and opacity (GPU-accelerated)
- Avoid paint-triggering animations (width/height)
- Use `will-change: transform` for animated elements
- Lazy load lower-priority images
- Cache SVG assets aggressively
- Minify SVG where possible (but maintain readability)

## Accessibility Checklist

### Color & Contrast
- ✅ All text meets WCAG AA (4.5:1 for body, 3:1 for graphics)
- ✅ No information conveyed by color alone
- ✅ Links are underlined or clearly distinguished
- ✅ Interactive elements have clear focus states

### Semantic HTML
- ✅ Headings use proper hierarchy (h1 > h2 > h3)
- ✅ Images have meaningful alt text
- ✅ Links have descriptive text
- ✅ Tables use `<th>` for headers
- ✅ Lists use semantic `<ul>`, `<ol>`, `<li>`

### Interactive Elements
- ✅ All buttons/links keyboard accessible (Tab navigation)
- ✅ Focus indicators visible (2px outline minimum)
- ✅ Buttons have `title` attributes for context
- ✅ Proper ARIA labels where needed

### Motion & Animation
- ✅ All animations respect `prefers-reduced-motion`
- ✅ No autoplay videos or animations
- ✅ Animations don't distract from content
- ✅ No flashing content (>3 times/second)

### Screen Reader Compatibility
- ✅ Semantic HTML structure
- ✅ Form labels properly associated
- ✅ Image alt text is descriptive
- ✅ Skip navigation links present (if applicable)
- ✅ Landmarks properly defined

## Code Quality Standards

### SVG Best Practices
- ✅ Use `viewBox` for responsive scaling
- ✅ Define gradients and filters in `<defs>`
- ✅ Use CSS for animations (not inline `animate` when possible)
- ✅ Optimize paths and remove unnecessary elements
- ✅ Use meaningful class names for styled elements

### CSS Best Practices
- ✅ Use CSS variables for colors
- ✅ Use meaningful animation names
- ✅ Organize styles logically (layout, then styling)
- ✅ Avoid `!important` flags
- ✅ Keep specificity low

### Markdown Best Practices
- ✅ Use proper heading hierarchy
- ✅ Include meaningful alt text for images
- ✅ Use semantic HTML in markdown (where supported)
- ✅ Link text describes destination
- ✅ Tables have clear headers

## Fallback Strategy

### External Service Failures
When GitHub stats, contribution graphs, or other external images fail:

1. **Automatic Fallback**
   - Browser loads `<source>` elements in order
   - Falls back to `<img src="./assets/fallback.svg">`
   - No broken image icons shown

2. **Graceful Degradation**
   - Fallback SVGs use same color scheme
   - Statistics still visible with estimated data
   - No functionality loss
   - Visual consistency maintained

3. **Offline Experience**
   - Profile fully viewable without external services
   - All critical information self-hosted
   - Links to external profiles still available
   - Performance not degraded

## Browser Support

### Tested On
- Chrome 90+
- Firefox 88+
- Safari 14+
- Edge 90+

### Features Used
- CSS animations and transitions
- SVG filters and gradients
- Modern CSS (flexbox, grid)
- Picture element for responsive images
- Media queries (including `prefers-reduced-motion`)

### Fallbacks Provided
- Static SVGs for animations
- Regular images for unsupported formats
- Basic styling for older browsers
- Keyboard navigation as primary interaction method

## Design Decisions & Rationale

### Why Cyberpunk Theme?
- Reflects personal brand identity
- Professional yet distinctive
- High contrast aids accessibility
- Modern and engaging
- Cybersecurity background alignment

### Why SVG for Assets?
- Scalable to any resolution
- Small file size (better than raster)
- CSS animations possible
- Responsive without media queries
- Animatable inline

### Why Fallback System?
- External services can fail
- Offline accessibility
- Performance independence
- User experience consistency
- Professional reliability

### Why Emphasis on Accessibility?
- Inclusive design is good design
- No assumptions about user capabilities
- WCAG 2.1 AA is industry standard
- Improves SEO
- Demonstrates professionalism

## Contributing Guidelines

When modifying this design system:

1. **Color Changes**: Update all references, maintain contrast ratios
2. **Typography Changes**: Test readability at all sizes
3. **Animation Changes**: Verify `prefers-reduced-motion` compatibility
4. **Asset Changes**: Maintain aspect ratios, test responsiveness
5. **Documentation**: Update this file before deployment

## Version History

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2024-08-14 | Initial design system with cyberpunk theme, animations, fallbacks |

---

**Design System Owner**: Jeremiah Carlton  
**Last Updated**: 2024-08-14  
**Status**: ✅ Production Ready
