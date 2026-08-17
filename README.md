# @infogata/shadcn-vite-theme-provider

A React dark mode theme provider based on the [shadcn/ui](https://ui.shadcn.com/docs/dark-mode/vite) pattern for Vite applications.

## Installation

```bash
npm install @infogata/shadcn-vite-theme-provider
```

## Usage

### Wrap your app with ThemeProvider

```tsx
import { ThemeProvider } from "@infogata/shadcn-vite-theme-provider";

function App() {
  return (
    <ThemeProvider defaultTheme="system" storageKey="vite-ui-theme">
      <YourApp />
    </ThemeProvider>
  );
}
```

### Use the useTheme hook

```tsx
import { useTheme } from "@infogata/shadcn-vite-theme-provider";

function ThemeToggle() {
  const { theme, setTheme } = useTheme();

  return (
    <button onClick={() => setTheme(theme === "dark" ? "light" : "dark")}>
      Toggle theme
    </button>
  );
}
```

### Example: Dropdown theme selector

```tsx
import { useTheme } from "@infogata/shadcn-vite-theme-provider";

function ModeToggle() {
  const { setTheme } = useTheme();

  return (
    <select onChange={(e) => setTheme(e.target.value as "light" | "dark" | "system")}>
      <option value="light">Light</option>
      <option value="dark">Dark</option>
      <option value="system">System</option>
    </select>
  );
}
```

## API

### ThemeProvider

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `children` | `React.ReactNode` | - | Child components |
| `defaultTheme` | `"light" \| "dark" \| "system"` | `"system"` | Default theme |
| `storageKey` | `string` | `"vite-ui-theme"` | localStorage key for persistence |

### useTheme

Returns an object with:

| Property | Type | Description |
|----------|------|-------------|
| `theme` | `"light" \| "dark" \| "system"` | Current theme |
| `setTheme` | `(theme: Theme) => void` | Function to change theme |

## Types

```typescript
import type { Theme, ThemeProviderProps, ThemeProviderState } from "@infogata/shadcn-vite-theme-provider";
```

## How it works

- Adds `dark` or `light` class to `document.documentElement`
- Persists theme selection to localStorage
- Respects system preference when set to `"system"`
- Works with Tailwind CSS dark mode (`darkMode: "class"`)

## Releasing

Bump the version locally (this also creates the tag), then push it — CI builds,
tests, publishes to npm, and cuts a GitHub Release:

```bash
npm version <patch|minor|major>
git push --follow-tags
```

Publishing uses npm OIDC trusted publishing, so there is no `NPM_TOKEN` secret
and provenance attestations are generated automatically. This repo and
`.github/workflows/publish.yml` must be registered once as a trusted publisher
under the package's npm settings.

## License

MIT
