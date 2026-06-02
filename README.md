# Air Force School Avadi - Website Template

This is the modernized, static website template for Air Force School Avadi, rebuilt from the ground up for maximum speed, security, and mobile responsiveness.

## Tech Stack
- **Framework**: [Astro](https://astro.build) (Outputs pure HTML/CSS without runtime JavaScript, making it inherently secure and incredibly fast).
- **Styling**: [Tailwind CSS v4](https://tailwindcss.com/) (Rapid UI development via utility classes).

## Why This Approach?
The previous website relied on outdated scripts (like MooTools from 2007) and suffered from SEO and security issues (including unauthorized scraped pages). This new template:
1. **Requires no database**: Eliminating SQL injection and CMS hacking risks.
2. **Is fully responsive**: Works perfectly on mobile phones, tablets, and desktops.
3. **Is easy to host**: The final build is just HTML/CSS. It can be hosted anywhere for free (GitHub Pages, Netlify, Cloudflare Pages, or traditional cPanel).

## How to Edit Content

The website content is located in the `src/pages/` directory. Each file represents a webpage:
- `index.astro`: Homepage
- `about.astro`: About Us
- `academics.astro`: Academics
- `admission.astro`: Admissions
- `facilities.astro`: Facilities
- `contact.astro`: Contact Us
- `gallery.astro`: Gallery
- `notices.astro`: Notices and Circulars

To change text, simply open the corresponding `.astro` file in any text editor, locate the text you wish to change, update it, and save the file.

## How to Run Locally

If you wish to run the site on your computer before deploying:

1. Install [Node.js](https://nodejs.org/).
2. Open a terminal in this folder and run:
   ```bash
   npm install
   ```
3. To start the local server:
   ```bash
   npm run dev
   ```
4. Open your browser and go to `http://localhost:4321`.

## How to Publish (Build)

When you are ready to publish the website to your live server:

1. Run the build command:
   ```bash
   npm run build
   ```
2. This will generate a new folder called `dist/`.
3. Take all the contents *inside* the `dist/` folder and upload them to your web server (via FTP or cPanel File Manager) replacing the old files.

## Changing the Header or Footer

The Header and Footer are shared across all pages. You only need to change them in one place:
- **Header**: `src/components/Header.astro` (Update menu links or logos here).
- **Footer**: `src/components/Footer.astro` (Update school address or phone number here).

## Updating Images
All images and documents are stored in the `public/` directory.
- For example, the logo is located at `public/images/logo.png`.
- Simply replace the image file with a new one using the *exact same filename* to update it across the site.
