# Agent Instructions

## Build & Test
- **Type**: Static HTML/CSS/JS website. No build step required.
- **Local Server**: Use a simple HTTP server to preview.
  - Python: `python -m http.server 8000`
  - Node: `npx serve .`
- **Testing**: Manual verification in browser. Open `index.html`.

## Architecture & Structure
- **Root**: Contains main pages (`index.html`, `imoveis.html`, `contato.html`) and documentation.
- **Assets**: `assets/` contains `css/` (styles), `js/` (logic), and `img/` (images).
- **Properties**: Individual property pages (e.g., `imovel-1.html`) usually live in the root or `imoveis/` folder.
  - **Note**: Ensure links in `imoveis.html` match the actual file location of the property pages.
- **Guide**: Follow `GUIA_ADICIONAR_IMOVEL.md` strictly when adding new properties.

## Code Style & Conventions
- **HTML**: Semantic HTML5. Use `<article>` for property cards.
- **CSS**: Use CSS variables defined in `root` (e.g., `--color-accent`). 
- **JS**: Vanilla JavaScript (ES6+). `DOMContentLoaded` setup in `main.js`.
- **Formatting**: Indent with 4 spaces. Keep HTML structure clean and readable.
- **Images**: High quality images in `assets/img/`. Use explicit `alt` text.
- **Currency**: Format prices as `R$ X.XXX.XXX` (Brazilian Real).
- **Naming**: Kebab-case for files (`imovel-villa-lobos.html`) and CSS classes (`property-card`).

## Firebase Integration
- **Status**: Integrated for contact form and property inquiries
- **Setup**: Follow `GUIA-FIREBASE-RAPIDO.md` for quick setup or `SETUP-FIREBASE.md` for detailed guide
- **Collections**:
  - `contacts` - Form submissions from `/contato.html`
  - `property_inquiries` - Property clicks with button attribute `data-inquiry-btn`
- **Config File**: `assets/js/firebase-config.js` (must be updated with your Firebase credentials)
- **Modules**:
  - `firebase-config.js` - Core Firebase setup and functions
  - `property-inquiry.js` - Property tracking on individual pages
- **Features**: Auto-timestamp, IP capture, fallback on error (doesn't block user actions)

## Workflows
- **Adding Properties**:
  1. Create new HTML file from `TEMPLATE-IMOVEL-FIREBASE.html` (or `TEMPLATE-IMOVEL-INDIVIDUAL.html` if not using Firebase)
  2. Add inquiry button with `data-inquiry-btn`, `data-property-id`, and `data-property-name` attributes
  3. Include Firebase property inquiry script: `<script type="module"> import { initPropertyInquiry } from '../assets/js/property-inquiry.js'; initPropertyInquiry(); </script>`
  4. Add card entry to `imoveis.html` grid.
  5. Use "Exclusivo" tag where appropriate.

- **Firebase Contact Form Setup** (already done in `contato.html`):
  - Form data auto-saves to `contacts` collection
  - Falls back to mailto if Firebase unavailable
  - No additional setup needed for contact page
