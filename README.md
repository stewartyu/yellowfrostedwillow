# Yellow Frosted Willow

Source for [www.yellowfrostedwillow.com](https://www.yellowfrostedwillow.com), built with [Astro](https://astro.build).

## Develop

    npm install
    npm run dev

Open [http://localhost:4321](http://localhost:4321).

## Checks

Pull requests run `.github/workflows/ci.yml`: type-check (`npm run check`), build, and an internal link check.

## Deploy

Pushing to `master` builds the site and deploys it to GitHub Pages via `.github/workflows/deploy.yml`.
To check a production build locally: `npm run build && npm run preview`.
