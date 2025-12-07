# AECTURA Website

A boutique digital consultancy website built with Eleventy and Decap CMS, deployed via Azure Static Web Apps.

## Quick Start

```bash
# Install dependencies
npm install

# Start development server
npm start

# Build for production
npm run build
```

The site will be available at `http://localhost:8080`.

## Project Structure

```
aectura-website/
├── src/
│   ├── _data/              # Global data files (site.json)
│   ├── _includes/          # Partial templates (header, footer)
│   ├── _layouts/           # Page layouts
│   ├── admin/              # Decap CMS configuration
│   ├── assets/
│   │   ├── css/            # Stylesheets
│   │   ├── js/             # JavaScript
│   │   └── images/         # Images and media
│   ├── insights/           # Blog/thought leadership posts
│   ├── services/           # Individual service pages
│   ├── case-studies/       # Case study content
│   └── *.njk               # Main pages (index, about, services, etc.)
├── .github/
│   └── workflows/          # GitHub Actions for Azure deployment
├── .eleventy.js            # Eleventy configuration
├── staticwebapp.config.json # Azure Static Web Apps config
└── package.json
```

## Content Management

The site uses Decap CMS for content management. Access the CMS at `/admin` once deployed.

### Content Types

| Collection | Location | Description |
|------------|----------|-------------|
| Insights | `src/insights/` | Blog posts and thought leadership |
| Services | `src/services/` | Individual service detail pages |
| Case Studies | `src/case-studies/` | Client work examples |
| Settings | `src/_data/site.json` | Site metadata and navigation |

### Adding Content Locally

Create markdown files directly in the appropriate folder:

```markdown
---
layout: insight.njk
title: "Your Post Title"
date: 2024-12-01
category: Strategy
excerpt: "Brief description for listings"
---

Your content here...
```

## Deployment

### Azure Static Web Apps Setup

1. Create a new Static Web App in Azure Portal
2. Connect to your GitHub repository
3. Azure will auto-detect the configuration from `staticwebapp.config.json`
4. Add the deployment token to GitHub Secrets as `AZURE_STATIC_WEB_APPS_API_TOKEN`

### GitHub Actions

The workflow in `.github/workflows/azure-static-web-apps.yml` handles:
- Building the Eleventy site on push to `main`
- Deploying to Azure Static Web Apps
- Creating preview environments for pull requests

## Decap CMS Authentication

For Decap CMS to work with GitHub:

1. **Option A: Netlify Identity** (if using Netlify for auth proxy)
   - Enable Netlify Identity on a Netlify site
   - Update `backend.base_url` in `src/admin/config.yml`

2. **Option B: Custom OAuth** (recommended for Azure)
   - Set up an OAuth application in GitHub
   - Create an Azure Function or external service for OAuth flow
   - Update the `auth_endpoint` in `src/admin/config.yml`

3. **Option C: Local Development**
   - Uncomment `local_backend: true` in `src/admin/config.yml`
   - Run `npx decap-server` in a separate terminal

## Customisation

### Brand Tokens

Update CSS custom properties in `src/assets/css/main.css`:

```css
:root {
  --color-accent: #1e3a5f;      /* Primary brand colour */
  --color-ink: #0f1419;          /* Text colour */
  --font-display: 'Instrument Serif', serif;
  --font-body: 'DM Sans', sans-serif;
}
```

### Adding New Content Types

1. Create a folder in `src/` (e.g., `src/sectors/`)
2. Add a directory data file (e.g., `sectors.json`) with default layout
3. Add the collection to `src/admin/config.yml`
4. Create a listing page if needed

### Navigation

Edit `src/_data/site.json` to update navigation items:

```json
{
  "navigation": [
    { "label": "Home", "url": "/" },
    { "label": "About", "url": "/about/" },
    { "label": "Services", "url": "/services/" },
    { "label": "Insights", "url": "/insights/" },
    { "label": "Contact", "url": "/contact/" }
  ]
}
```

## Development Notes

- Eleventy rebuilds automatically when files change
- CSS uses custom properties for easy theming
- All layouts extend `base.njk`
- The site is fully responsive with mobile navigation

## License

Private - All rights reserved.
