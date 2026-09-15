# Atlas BD

Atlas BD is a map first interactive geographic atlas for exploring universities across Bangladesh. It presents the country as a calm, holographic cartographic surface: public and private institutions resolve from signals into labelled markers as the map zooms in, while profiles, search, filters and live counts keep the experience useful rather than decorative.

## Features

- Map-first Bangladesh overview with a stylized geographic silhouette, division grid and subtle terrain treatment.
- Zoom-sensitive signals: distant universities read as glowing dots; closer views reveal logo-like initials and names.
- Smooth focus behavior when a marker or search result is selected.
- Search by university name, acronym, city, district or division.
- Combined filters for university type, category and division.
- Dynamic statistics and compact legend derived from the dataset.
- Responsive profile panel that becomes a bottom sheet on small screens.
- Official website and Google Maps links on every profile.
- Accessible buttons, labels, focusable SVG markers and reduced-motion support.

## Stack

- React 19 + TypeScript
- Vite
- Plain CSS with a small, intentional visual system (no runtime map API or API key required)
- SVG for the geographic surface and marker layer

The first release intentionally keeps the architecture static and deployment-friendly. The map projection is a lightweight local projection over a curated data file, which keeps the app fast and makes the visual system reliable in preview and on static hosting.

## Run locally

```bash
pnpm install
pnpm dev
```

Then open the local URL printed by Vite. Create a production build with:

```bash
pnpm build
pnpm preview
```

No environment variables are required for the current static release. If the data layer is moved to a database or remote storage in a future release, add a `.env.example` before introducing secrets.

## Data model and provenance

University records live in `src/data.ts` and follow a stable model: `id`, `name`, `shortName`, `type`, `category`, `division`, `district`, `city`, `address`, `latitude`, `longitude`, `establishedYear`, `logo`, `description`, `website`, `maps`, `source` and `lastVerified`.

The initial atlas focuses on a meaningful representative set of recognized public and private universities across Dhaka, Chattogram, Khulna, Rajshahi, Sylhet, Mymensingh and Barishal divisions. Facts, official links and campus locations were assembled from official university websites and cross-checked against commonly used map locations during development. Campus coordinates are intended for geographic discovery, not surveying-grade precision. The UI makes the last-verified date visible in each profile.

## Deployment

This repository is a Vite static site and can be deployed to GitHub Pages, Vercel, Netlify or any static host. The build output is `dist/`. Configure the host to serve `index.html` for the root route.

## Known limitations

The current version uses a stylized local SVG map rather than a live GIS tile source, so district boundaries are illustrative and the initial dataset is curated rather than exhaustive. The next production iteration should add a GeoJSON boundary layer, a larger UGC-validated university registry, an image CDN for official marks and server-backed dataset versioning.

## Future improvements

1. Replace the illustrative division grid with official division and district GeoJSON boundaries.
2. Add a verified UGC import pipeline with duplicate detection and review status.
3. Add clustering at national scale and richer campus imagery at close zoom.
4. Add keyboard shortcuts and shareable deep links for a selected university.
5. Add multilingual labels for Bangla-first discovery.
