# Theme Design - shadcn/ui for Sistem Raport Akademik

Tema custom untuk sistem raport dengan nuansa pendidikan Islam.

---

## 1. Warna Palette

### 1.1 Primary Colors (Sage Green)

| CSS Variable | Hex | Usage |
|--------------|-----|-------|
| `--primary` | `#5C8D6E` | Buttons, links, active states |
| `--primary-foreground` | `#FFFFFF` | Text on primary buttons |
| `--primary-light` | `#7CAD8E` | Hover states |
| `--primary-dark` | `#4A7358` | Active/pressed states |

### 1.2 Secondary Colors (Sand/Cream)

| CSS Variable | Hex | Usage |
|--------------|-----|-------|
| `--secondary` | `#F5E6D3` | Background accents, cards |
| `--secondary-foreground` | `#1E3A5F` | Text on secondary |
| `--secondary-light` | `#FAF3E8` | Hover states |
| `--secondary-dark` | `#E8D5BC` | Active states |

### 1.3 Accent Colors (Dark Navy)

| CSS Variable | Hex | Usage |
|--------------|-----|-------|
| `--accent` | `#1E3A5F` | Sidebar, headers |
| `--accent-foreground` | `#FFFFFF` | Text on accent |
| `--accent-light` | `#2D4A6F` | Hover states |
| `--accent-dark` | `#152C45` | Active states |

### 1.4 Neutral Colors

| CSS Variable | Hex | Usage |
|--------------|-----|-------|
| `--background` | `#FAFAFA` | Main page background |
| `--foreground` | `#1A1A1A` | Main text |
| `--muted` | `#F4F4F5` | Muted backgrounds |
| `--muted-foreground` | `#71717A` | Muted text |
| `--border` | `#E4E4E7` | Borders |
| `--input` | `#E4E4E7` | Input backgrounds |
| `--ring` | `#5C8D6E` | Focus rings |

### 1.5 Semantic Colors

| CSS Variable | Hex | Usage |
|--------------|-----|-------|
| `--destructive` | `#DC2626` | Error states |
| `--destructive-foreground` | `#FFFFFF` | Text on destructive |
| `--success` | `#16A34A` | Success states |
| `--warning` | `#F59E0B` | Warning states |

---

## 2. Tailwind Configuration

### 2.1 tailwind.config.ts

```typescript
import { fontFamily } from 'tailwindcss/defaultTheme'

export const theme = {
  extend: {
    colors: {
      // Primary - Sage Green
      primary: {
        DEFAULT: '#5C8D6E',
        foreground: '#FFFFFF',
        light: '#7CAD8E',
        dark: '#4A7358',
      },
      // Secondary - Sand/Cream
      secondary: {
        DEFAULT: '#F5E6D3',
        foreground: '#1E3A5F',
        light: '#FAF3E8',
        dark: '#E8D5BC',
      },
      // Accent - Dark Navy
      accent: {
        DEFAULT: '#1E3A5F',
        foreground: '#FFFFFF',
        light: '#2D4A6F',
        dark: '#152C45',
      },
      // Backgrounds
      background: '#FAFAFA',
      foreground: '#1A1A1A',
      muted: {
        DEFAULT: '#F4F4F5',
        foreground: '#71717A',
      },
      // Borders
      border: '#E4E4E7',
      input: '#E4E4E7',
      // Rings
      ring: '#5C8D6E',
    },
    fontFamily: {
      sans: ['Inter', ...fontFamily.sans],
      serif: ['Merriweather', ...fontFamily.serif],
    },
    borderRadius: {
      lg: '0.5rem',
      md: '0.375rem',
      sm: '0.25rem',
    },
  },
}
```

### 2.2 globals.css

```css
@tailwind base;
@tailwind components;
@tailwind utilities;

@layer base {
  :root {
    /* Primary - Sage Green */
    --primary: 142 40% 42%;
    --primary-foreground: 0 0% 100%;
    --primary-light: 142 40% 52%;
    --primary-dark: 142 40% 35%;

    /* Secondary - Sand/Cream */
    --secondary: 35 70% 88%;
    --secondary-foreground: 212 54% 24%;
    --secondary-light: 35 70% 94%;
    --secondary-dark: 35 70% 80%;

    /* Accent - Dark Navy */
    --accent: 212 54% 24%;
    --accent-foreground: 0 0% 100%;
    --accent-light: 212 54% 30%;
    --accent-dark: 212 54% 18%;

    /* Backgrounds */
    --background: 0 0% 98%;
    --foreground: 0 0% 10%;

    /* Muted */
    --muted: 240 5% 96%;
    --muted-foreground: 240 4% 46%;

    /* Borders */
    --border: 240 6% 90%;
    --input: 240 6% 90%;
    --ring: 142 40% 42%;

    /* Radius */
    --radius: 0.5rem;
  }
}

@layer base {
  * {
    @apply border-border;
  }
  body {
    @apply bg-background text-foreground;
  }
}
```

---

## 3. Component Styles

### 3.1 Button Variants

```typescript
const buttonVariants = cva(
  'inline-flex items-center justify-center rounded-md text-sm font-medium transition-colors focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring',
  {
    variants: {
      variant: {
        default: 'bg-primary text-primary-foreground hover:bg-primary/90',
        destructive: 'bg-destructive text-destructive-foreground hover:bg-destructive/90',
        outline: 'border border-input bg-background hover:bg-accent hover:text-accent-foreground',
        secondary: 'bg-secondary text-secondary-foreground hover:bg-secondary/80',
        ghost: 'hover:bg-accent hover:text-accent-foreground',
        link: 'text-primary underline-offset-4 hover:underline',
      },
      size: {
        default: 'h-10 px-4 py-2',
        sm: 'h-9 rounded-md px-3',
        lg: 'h-11 rounded-md px-8',
        icon: 'h-10 w-10',
      },
    },
    defaultVariants: {
      variant: 'default',
      size: 'default',
    },
  }
)
```

### 3.2 Card Styles

```tsx
// Default card style - Cream background
function Card({ className, ...props }) {
  return (
    <div
      className={cn(
        'rounded-lg border border-secondary bg-white text-foreground shadow-sm',
        className
      )}
      {...props}
    />
  )
}

// Alternative card with sand background
function CardSand({ className, ...props }) {
  return (
    <div
      className={cn(
        'rounded-lg border border-secondary bg-secondary/30 text-foreground shadow-sm',
        className
      )}
      {...props}
    />
  )
}
```

---

## 4. Layout Examples

### 4.1 Sidebar Navigation

```tsx
// Sidebar - Dark Navy
<aside className="bg-accent text-accent-foreground min-h-screen w-64 p-4">
  <nav className="space-y-2">
    <Link href="/dashboard" className="flex items-center gap-3 px-4 py-2 rounded-md hover:bg-accent-light">
      Dashboard
    </Link>
    <Link href="/students" className="flex items-center gap-3 px-4 py-2 rounded-md hover:bg-accent-light">
      Data Siswa
    </Link>
    <Link href="/grades" className="flex items-center gap-3 px-4 py-2 rounded-md hover:bg-accent-light">
      Input Nilai
    </Link>
  </nav>
</aside>
```

### 4.2 Main Content Area

```tsx
// Main content - Off white background
<main className="flex-1 bg-background p-6">
  <h1 className="text-2xl font-semibold text-foreground mb-6">Dashboard</h1>
  
  {/* Cards */}
  <div className="grid gap-4 md:grid-cols-3">
    <Card className="p-6">
      <h3 className="text-sm font-medium text-muted-foreground">Total Siswa</h3>
      <p className="text-3xl font-bold text-primary">150</p>
    </Card>
  </div>
</main>
```

### 4.3 Data Table

```tsx
// Table header - Secondary color
<TableHeader className="bg-secondary/50">
  <TableRow>
    <TableHead className="text-secondary-foreground">Nama</TableHead>
    <TableHead className="text-secondary-foreground">NIS</TableHead>
    <TableHead className="text-secondary-foreground">Kelas</TableHead>
  </TableRow>
</TableHeader>
```

---

## 5. Typography

### 5.1 Font Selection

| Usage | Font | Weights |
|-------|------|---------|
| Headings | Inter | 600, 700 |
| Body | Inter | 400, 500 |
| Arabic text | Amiri | 400 |
| UI Labels | Inter | 500 |

### 5.2 Font Sizes

```css
/* Tailwind classes */
text-xs     /* 0.75rem */
text-sm     /* 0.875rem */
text-base   /* 1rem */
text-lg     /* 1.125rem */
text-xl     /* 1.25rem */
text-2xl    /* 1.5rem */
text-3xl    /* 1.875rem */
text-4xl    /* 2.25rem */
```

---

## 6. Installation Instructions

### 6.1 Initialize shadcn/ui

```bash
# Initialize shadcn (pilih default saat diminta)
npx shadcn@latest init

# Install komponen yang dibutuhkan
npx shadcn@latest add button card input table form dropdown-menu dialog toast
```

### 6.2 Apply Theme

1. Copy `globals.css` content ke `src/app/globals.css`
2. Copy tailwind config ke `tailwind.config.ts`
3. Restart dev server

---

## 7. Color Preview

```
┌─────────────────────────────────────────────────────────┐
│  PRIMARY: #5C8D6E (Sage Green)                         │
│  ████████░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │
│                                                         │
│  SECONDARY: #F5E6D3 (Sand/Cream)                       │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │
│                                                         │
│  ACCENT: #1E3A5F (Dark Navy)                          │
│  ██████████████████████████████████████████████████    │
│                                                         │
│  BACKGROUND: #FAFAFA (Off White)                        │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │
└─────────────────────────────────────────────────────────┘
```

---

## 8. References

- [shadcn/ui Documentation](https://ui.shadcn.com)
- [Tailwind CSS](https://tailwindcss.com)
- [CSS Variables](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_custom_properties)

---

**Theme Design Version:** 1.0
**Created:** 7 Februari 2026
