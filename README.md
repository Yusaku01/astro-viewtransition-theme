# astro-viewtransition-theme

Astro theme toggle components with view transitions support.

## Install

```sh
npm install astro-viewtransition-theme
```

## Usage

```astro
---
import { ThemeInit, ThemeToggle } from 'astro-viewtransition-theme';
---

<html lang="en">
	<head>
		<ThemeInit />
	</head>
	<body>
		<ThemeToggle />
	</body>
</html>
```

### Custom button

```astro
---
import { ThemeInit, ThemeToggle, ThemeButton } from 'astro-viewtransition-theme';
---

<ThemeInit />
<ThemeToggle>
	<ThemeButton />
</ThemeToggle>
```

## Notes

- The current theme is stored in `localStorage` under the `theme` key.
- The active theme is applied via `data-theme` on the `<html>` element.
- `ThemeToggle` listens for `astro:before-swap` and `astro:page-load` to keep the theme during view transitions.
- Customize the button via CSS variables:
  - `--toggle-track`
  - `--toggle-thumb`
  - `--toggle-icon`
  - `--accent` (focus ring)
