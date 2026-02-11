# LittleLink - Project Context

LittleLink is a DIY, self-hosted, and lightweight alternative to services like Linktree. It is designed to be a "link in bio" tool that is easy to customize, high-performing, and privacy-focused.

## Project Overview

- **Purpose:** Provide a simple, customizable landing page for social links.
- **Philosophy:** Minimalism and performance. It avoids large frameworks (no React, Vue, etc.) in favor of vanilla HTML and CSS.
- **Performance:** Achieves 100/100 scores in Google PageSpeed Insights for Performance, Accessibility, Best Practices, and SEO.
- **Accessibility:** Built-in support for `light`, `dark`, and `auto` (system-preference) themes, with focus states and semantic HTML.

## Key Technologies

- **Frontend:** HTML5, CSS3 (Vanilla).
- **Icons:** SVG icons stored in `images/icons/`.
- **Fonts:** "Open Sans" (self-hosted in `fonts/`).
- **Deployment:** 
  - **Docker:** Nginx-based containerization (`docker/`).
  - **Cloudflare Workers:** Static asset hosting via Wrangler (`wrangler.toml`).
  - **DigitalOcean:** Deployment template (`.do/`).

## Project Structure

- `index.html`: The main entry point. Users customize this file to add their personal links and branding.
- `css/`:
  - `style.css`: Core layout, typography, and theme system.
  - `brands.css`: Contains styles for over 100+ branded buttons (e.g., `.button-amazon`, `.button-github`).
  - `reset.css`: Standard CSS reset.
- `images/`:
  - `avatar.png`: Default profile picture.
  - `icons/`: SVG brand icons used within buttons.
- `docker/`: Dockerfile and compose configuration for hosting with Nginx.
- `wrangler.toml`: Configuration for deploying to Cloudflare Workers.
- `privacy.html`: A template for a privacy policy page.

## Development and Running

### Local Development
Since this is a static project, you can simply open `index.html` in any web browser to view changes.

### Using Docker
For a containerized local environment or production hosting:
```bash
# Start the development environment (with live volume mounting)
docker compose -f docker/compose.yaml up
```
The site will be available at `http://localhost:8080`.

### Using Cloudflare Workers
```bash
# Preview locally
npx wrangler dev

# Deploy to Cloudflare
npx wrangler deploy
```

## Customization Conventions

### Themes
Themes are controlled by classes on the `<html>` tag in `index.html`:
- `theme-auto`: Respects system preferences.
- `theme-light`: Forces light mode.
- `theme-dark`: Forces dark mode.

### Adding/Modifying Buttons
Buttons follow a specific HTML pattern:
```html
<a class="button button-brandname" href="URL" target="_blank" rel="noopener" role="button">
  <img class="icon" aria-hidden="true" src="images/icons/brand.svg" alt="Brand Logo">
  Brand Name
</a>
```
Custom button colors are defined in `css/brands.css` using CSS variables:
```css
.button-brandname {
  --button-background: #HEXCODE;
  --button-text: #HEXCODE;
}
```

### Avatar Styles
The profile image supports three rounding options:
- `avatar--rounded`: Full circle.
- `avatar--soft`: Slightly rounded corners.
- `avatar--none`: Square image.

## Maintenance and Contribution

- **Linting:** The project uses `pre-commit` for basic file linting.
- **Versioning:** Refer to `VERSION.md` for the current version (`v3.10.0`) and change history.
- **Accessibility:** Always ensure high contrast ratios. Use the `inverse stroke` technique if a button color lacks contrast against the background in specific themes.
- **New Brands:** Follow the guidelines in the [Official Wiki](https://github.com/sethcottle/littlelink/wiki/Submitting-a-new-brand-to-LittleLink) before adding new branded buttons.
