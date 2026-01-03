# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static HTML website for Rahaman Events Co., a photo booth and event rental business serving NYC, Nassau County, and Suffolk County. The site is built with vanilla HTML, CSS, and JavaScript - no frameworks or build tools.

## Development Commands

### Local Development
Open any HTML file directly in a browser - no build step required.

### Deployment
```bash
./deploy.sh
```
This script pushes to GitHub and SSHs into the DigitalOcean server to pull changes. Enter the server password when prompted.

### Manual Deployment (if script fails)
```bash
git push origin main
ssh root@104.131.119.134 "cd /var/www/html && git pull origin main"
```

## Architecture

### File Structure
- `index.html`, `services.html`, `gallery.html`, `backdrops.html`, `about.html`, `contact.html` - Main pages
- `assets/css/styles.css` - Single stylesheet with CSS variables for theming
- `assets/js/scripts.js` - Vanilla JS for interactions (mobile menu, scroll effects, lightbox, form validation)
- `assets/images/gallery/` - Event photos
- `assets/images/backdrops/` - Backdrop product photos

### CSS Variables (defined in :root)
- `--primary-blue: #004aad` - Headers, navigation, trust elements
- `--accent-red: #e55267` - CTAs, highlights
- `--pure-white: #ffffff` - Backgrounds
- Typography: League Spartan (headers), Lora (body) via Google Fonts

### Contact Form
Uses Formspree (https://formspree.io/f/xojqnklz) for form submissions. The form POSTs to this endpoint and emails are forwarded to info@rahamaneventsco.com.

## Infrastructure

- **Hosting**: DigitalOcean VPS at 104.131.119.134
- **Web Server**: Apache 2.4 on Ubuntu 24.04 LTS
- **SSL**: Let's Encrypt (auto-renewing via Certbot)
- **Domain**: rahamaneventsco.com (managed at Porkbun)
- **Web Root**: /var/www/html/

## Key Patterns

### Adding Gallery Photos
1. Resize images to 1200px max width, under 500KB
2. Save to `assets/images/gallery/`
3. Update `gallery.html` with img tags and overlay content

### Updating Prices
Search and replace across `services.html` and `index.html` - prices appear in `.package-price` elements.

### Responsive Design
Mobile-first with `@media` queries in styles.css. Test mobile menu toggle and responsive grids when making layout changes.
