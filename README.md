# Midnight Video

A spooky random horror movie picker. Set your limits, hit **Scare Me**, and the shelf picks tonight's feature.

**Live site:** `https://empty-astronaut.github.io/midnight-video/`

## What it does

Pick your guards first, then let the shelf decide:

- **Release years:** set an earliest and latest year
- **IMDb rating:** only films at or above a minimum score
- **Runtime:** cap how long the movie can run
- **Subgenres:** 17 to choose from (slasher, folk horror, found footage, cosmic dread, home invasion, and more). Match **Any** of the ones you pick, or require **All** of them.
- **Skip seen:** mark films as seen and leave them out of future picks

A live counter shows how many tapes match your guards. If nothing matches, the shelf tells you to loosen up.

Each pick shows the rating, year, runtime, director, subgenre tags and a one-line synopsis, with links to IMDb and JustWatch. There's a short history of your earlier picks, a synthesized jump-scare sound (toggle it off in the header), and fog, film grain and a flickering neon sign. Animations switch off automatically if your system is set to reduce motion.

## The movie list

The list is built into the page: 458 horror films from *Nosferatu* (1922) to 2025. It isn't pulled from IMDb live. IMDb has no free public API, and a static page can't call most third-party APIs without exposing a key.

Ratings are approximate IMDb scores and drift over time. Use the IMDb link on each pick to see the current number.

## Run it

It's one static file with no build step and no dependencies to install.

- **Locally:** open `index.html` in a browser.
- **GitHub Pages:** go to **Settings > Pages**, set **Source** to "Deploy from a branch", choose your main branch and the `/ (root)` folder, and save. The file must be named `index.html` and sit at the top level of the repo.

Fonts (Pirata One, Special Elite, Spectral) load from Google Fonts, so the page needs an internet connection to look right.

## Add or edit movies

All the films live in one block near the top of the script in `index.html`, in a constant called `RAW`. Each film is one line with seven fields separated by pipes:

```
Title|Year|Rating|Runtime|tags|Director|Logline
```

For example:

```
The Thing|1982|8.2|109|scifi,creature,body|John Carpenter|An Antarctic research crew learns the thing that thawed out can look like any of them.
```

Rules:

- Runtime is in minutes. Rating is a number like `7.4`.
- Tags are comma-separated with no spaces. Use only these keys: `slasher`, `supernatural`, `possession`, `haunted`, `folk`, `witch`, `body`, `creature`, `zombie`, `vampire`, `psych`, `scifi`, `cosmic`, `found`, `invasion`, `survival`, `comedy`.
- Don't use a `|` inside a field.
- Skip any title and year that's already in the list, so a film doesn't show up twice.
- The year slider range adjusts on its own to the oldest and newest films.

Commit the change and GitHub Pages redeploys in a minute or two.

## Saved in your browser

Your filters, seen list, pick history and sound setting are saved with `localStorage`, so they stick around between visits on the same browser and device. Nothing is sent anywhere. Clearing site data resets them, and the **Reset guards** button restores the default filters.

## Credits

Built with plain HTML, CSS and JavaScript. Sound effects are generated in the browser with the Web Audio API, so there are no audio files. Film details are not affiliated with or sourced live from IMDb or JustWatch, which are linked for convenience only.
