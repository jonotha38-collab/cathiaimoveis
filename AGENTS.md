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

## Workflows
- **Adding Properties**:
  1. Create new HTML file from `TEMPLATE-IMOVEL-INDIVIDUAL.html` or copy an existing one.
  2. Add card entry to `imoveis.html` grid.
  3. Use "Exclusivo" tag where appropriate.
