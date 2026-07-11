# ConnectHub Design System

## Overview

ConnectHub uses a modern, clean design inspired by contemporary mobile apps while maintaining original branding and aesthetics. The design prioritizes user experience with smooth animations, intuitive navigation, and accessible interfaces.

## Color Palette

### Primary Colors
- **Dark Background**: `#1a1a2e` - Main app background
- **Accent Primary**: `#7c3aed` - Primary interactive elements (purple)
- **Accent Secondary**: `#ec4899` - Secondary actions (pink)

### Neutral Colors
- **Text Primary**: `#f5f5f5` - Main text
- **Text Secondary**: `#a3a3a3` - Secondary text
- **Surface 1**: `#252537` - Card backgrounds
- **Surface 2**: `#2d2d42` - Input fields
- **Border**: `#3f3f54` - Dividers and borders

### Status Colors
- **Success**: `#10b981` - Confirmations, online status
- **Warning**: `#f59e0b` - Alerts, warnings
- **Error**: `#ef4444` - Errors, offline status
- **Info**: `#3b82f6` - Information

### Theme Variants
- **Light Mode**: White backgrounds with dark text
- **Dark Mode** (default): Dark backgrounds with light text
- **AMOLED**: Pure black `#000000` background for OLED screens

## Typography

### Font Family
- **Primary**: Inter or system default sans-serif
- **Monospace**: JetBrains Mono (for code snippets)

### Font Sizes & Weights
- **Display**: 32px, Bold (titles/headers)
- **Heading 1**: 28px, Bold (major sections)
- **Heading 2**: 24px, Semi-Bold (subsections)
- **Heading 3**: 20px, Semi-Bold (cards)
- **Body Large**: 16px, Regular (main content)
- **Body**: 14px, Regular (standard text)
- **Body Small**: 12px, Regular (secondary text)
- **Caption**: 11px, Regular (metadata)

### Line Height
- **Headings**: 1.2
- **Body**: 1.5
- **Captions**: 1.4

## Spacing System

8px base unit (8, 16, 24, 32, 48, 64px)

### Common Spacing
- **XS**: 4px
- **S**: 8px
- **M**: 16px
- **L**: 24px
- **XL**: 32px
- **2XL**: 48px
- **3XL**: 64px

## Border Radius

- **Small**: 4px - Form inputs, small components
- **Medium**: 8px - Cards, buttons
- **Large**: 12px - Modals, major containers
- **XL**: 16px - Server/channel icons
- **Full**: 9999px - Avatars, pill buttons

## Components

### Buttons
- **Primary**: Solid accent color background
- **Secondary**: Outlined with accent color
- **Tertiary**: Ghost/text only
- **Danger**: Red for destructive actions
- **Disabled**: Reduced opacity, no interaction

### Cards
- Border radius: 12px
- Background: Surface 1
- Padding: 16px
- Shadow: Subtle elevation
- Border: 1px, Border color

### Input Fields
- Border radius: 8px
- Background: Surface 2
- Border: 1px, Border color
- Padding: 12px 16px
- Focus state: Accent color border, subtle glow
- Placeholder text: Secondary text color

### Navigation
- Bottom tab bar with 5 sections
- Active tab: Accent color icon/text
- Inactive tab: Secondary text color
- Height: 64px (iOS) / 56px (Android)

### Modals & Sheets
- Border radius: 16px (top)
- Background: Surface 1
- Scrim: Semi-transparent black overlay
- Elevation: High shadow

### Avatars
- Border radius: Full circle
- Sizes: 24px, 32px, 48px, 64px
- Placeholder: Initials or default icon
- Border: 2px, accent color (optional)

## Animations

### Transitions
- **Fast**: 150ms (hover effects, small components)
- **Standard**: 300ms (modal opens, screen transitions)
- **Slow**: 500ms (complex animations, transitions between major states)

### Easing
- **Standard**: cubic-bezier(0.4, 0, 0.2, 1)
- **Entrance**: cubic-bezier(0, 0, 0.2, 1)
- **Exit**: cubic-bezier(0.4, 0, 1, 1)

### Common Animations
- Fade in/out: 200ms opacity transition
- Scale: 250ms transform transition (0.95 to 1.0)
- Slide: 300ms translate transition
- Bounce: Spring animation for feedback

## Icons

- **Style**: Outline icons with 2px stroke weight
- **Size**: 24px (standard), 16px (compact), 32px (large)
- **Color**: Inherit from text color or custom
- **Library**: Feather Icons or custom SVGs

## Interactive States

### Buttons
- **Default**: Solid color
- **Hover**: 10% opacity increase
- **Active/Pressed**: 20% opacity decrease
- **Disabled**: 50% opacity

### Input Fields
- **Idle**: Border color
- **Focus**: Accent border + subtle glow
- **Filled**: Text color
- **Error**: Error color border + error message
- **Success**: Success color check mark

### Cards
- **Default**: Normal shadow
- **Hover**: Increased shadow, slight lift (web only)
- **Active**: Accent color border highlight

## Responsive Design

### Breakpoints
- **Mobile**: 320px - 767px (phones)
- **Tablet**: 768px - 1199px (tablets)
- **Desktop**: 1200px+ (larger screens)

### Mobile-First Approach
- Design for 375px (iPhone SE) as baseline
- Test on 320px (minimum), 428px (modern phones)
- Support both portrait and landscape

## Accessibility

- **Color Contrast**: WCAG AA minimum (4.5:1 for text)
- **Touch Targets**: Minimum 44x44px for interactive elements
- **Focus Indicators**: Clear 2px border with accent color
- **Text Scaling**: Support 100-200% font scaling
- **Icons + Text**: All important icons have text labels
- **Motion**: Respect prefers-reduced-motion

## Dark Mode Implementation

- System preference detection
- Manual toggle in settings
- Persistent user choice
- Auto-switching at sunrise/sunset (optional)
- All colors adapted for WCAG compliance in dark mode

## Design Files

- Figma: [ConnectHub Design System]
- Asset library with all components
- Icon sets (light and dark)
- Color tokens
- Responsive layout guides

## Development Guidelines

### CSS-in-JS Variables
```
--color-primary: #7c3aed
--color-secondary: #ec4899
--color-success: #10b981
--color-error: #ef4444
--color-text-primary: #f5f5f5
--color-bg-primary: #1a1a2e
--radius-sm: 4px
--radius-md: 8px
--radius-lg: 12px
--spacing-xs: 4px
--transition-fast: 150ms
--transition-standard: 300ms
```

### Usage in Code
- Use design tokens consistently
- Don't hardcode color values
- Follow spacing system for margins/padding
- Apply standard transitions for state changes
- Test with theme toggle active

## Brand Voice

- **Friendly yet professional**
- **Clear and concise**
- **Approachable but trustworthy**
- **Encouraging and supportive**

---

For detailed component specifications, interactions, and design tokens, refer to the Figma design file.
