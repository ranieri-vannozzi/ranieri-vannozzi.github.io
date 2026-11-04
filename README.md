# ranierivannozzi.com

Source code of [ranierivannozzi.com](https://ranierivannozzi.com), the personal profile of Ranieri Vannozzi, tech lead and software architect.

The site is a single page online CV: overview, education, key skills, career, skills, personal projects, interests, the latest articles from the [HeroHubs](https://herohubs.it) blog and contacts.

## Tech stack

| Layer      | Technology                                                                                        |
| ---------- | ------------------------------------------------------------------------------------------------- |
| Framework  | [Astro 5](https://astro.build/)                                                                   |
| UI         | [Tailwind CSS 4](https://tailwindcss.com/), [React 19](https://react.dev/) for the icon component |
| Icons      | [react-icons](https://react-icons.github.io/react-icons/) (Font Awesome 6)                        |
| Images     | Astro image pipeline with [Sharp](https://sharp.pixelplumbing.com/), WebP output                  |
| Typography | Montserrat, self-hosted from `public/fonts/`                                                      |
| Analytics  | Google Analytics, loaded through [Partytown](https://partytown.qwik.dev/)                         |
| Hosting    | GitHub Pages, deployed by GitHub Actions                                                          |

## Content

All page content lives in JSON files under `src/config/`, one file per section, so updating the profile never requires touching the components.

| File             | Section                                                                    |
| ---------------- | -------------------------------------------------------------------------- |
| `config.json`    | Site title, profile name, designation, bio, metadata, analytics and footer |
| `overview.json`  | Overview                                                                   |
| `education.json` | Education                                                                  |
| `keys.json`      | Key skills                                                                 |
| `career.json`    | Career, one entry per role                                                 |
| `skills.json`    | Skills, grouped and rendered as tags                                       |
| `projects.json`  | Personal projects, with an optional `url` that adds an external link icon  |
| `interests.json` | Interests                                                                  |
| `writing.json`   | Latest articles: HeroHubs feed URL, blog link and number of articles       |
| `contacts.json`  | Contact email and social links                                             |
| `menu.json`      | Navigation anchors                                                         |
| `theme.json`     | Colors and font family, shared with the HeroHubs palette                   |

Each section is rendered by a component in `src/layouts/components/`, and `src/pages/index.astro` arranges them on the page. The profile photo is generated from the original at 1x, 2x and 3x densities, so it stays sharp on high-density screens.

The latest articles are read from the HeroHubs RSS feed at build time. If the feed cannot be reached the section is left empty and the build still succeeds.

## Local development

**Prerequisites:** Node.js 20, the version used by the deploy workflow, and npm.

```bash
npm ci            # install the exact dependencies from package-lock.json
npm run dev       # dev server on http://localhost:4321
npm run build     # production build in dist/
npm run preview   # serve the production build locally
npm run format    # format src/ with Prettier
```

The dev server reads `src/config/theme.json` only at startup: restart it after changing colors or fonts.

## Code formatting

[Prettier](https://prettier.io/) runs on every commit through a [Lefthook](https://lefthook.dev/) pre-commit hook, which formats the whole repository and stages the result.

## Deployment

The workflow in `.github/workflows/deploy.yml` builds the site and publishes `dist/` to the `gh-pages` branch, served by GitHub Pages on the domain in `CNAME`. It runs:

- on every push to `main`
- every day at 10:00 UTC, so the latest HeroHubs articles and the copyright year stay current without a new commit
- on demand from the Actions tab

Changes reach `main` through pull requests.

## License

The source code is released under the [MIT](./LICENSE) license, inherited from the [Hydrogen Astro](https://github.com/statichunt/hydrogen-astro) theme by Statichunt on which the site is based.

The personal content, including texts, career data and photos, is not covered by that license and remains © Ranieri Vannozzi, all rights reserved.
