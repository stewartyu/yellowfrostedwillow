# Notes for Claude

## Changes go through a pull request

Never push directly to `master`: every merge deploys the live site. Make changes on a branch,
open a pull request, and let Stewart review and merge it.

## After a PR merges: run the content smoke checks

Every merge to `master` deploys the live site (`.github/workflows/deploy.yml`, GitHub Pages).
After a merge, Stewart wants the content checks from the "Daily website smoke test" scheduled
task run against the live site. Certificate checks are not needed on merges.

- **If you are watching the PR and its merge event reaches you:** wait for the "Deploy to GitHub
  Pages" run on the merge commit to finish, then run the checks yourself and report the results.
- **Otherwise** (you only see the merge afterwards, or Stewart mentions merging): remind Stewart
  to have the checks run, and offer to run them right then.

The checks, read-only (report results, never change anything):

1. **Page:** https://www.yellowfrostedwillow.com loads over HTTPS with the title
   "Yellow Frosted Willow: The Anna May Wong Musical", the 1924 photo of Anna May Wong, the
   黃柳霜 name beside the title, the "In concert" section (Nov. 23 at Don't Tell Mama, with the Don't Tell Mama logo) with its
   "Get tickets" link, and "The story", "Featuring", "Music director & pianist" (Minhui Lee) and "Listen" sections. ("Listen" uses an
   embedded player, so it can look empty in fetched HTML; that's fine.)
2. **Images and links:** run the site-check Python script stored in the "Daily website smoke
   test" scheduled task's prompt (read it with the `list_triggers` / `get_trigger` tools), saved
   to the scratchpad and run with `python3 -I`. The script covers all four of Stewart's sites
   for the daily test; in the saved copy, remove every `SITES` entry except
   `"www.yellowfrostedwillow.com"` so it checks only this site, and change nothing else.
   Facebook/X and 401/403/429 responses are "couldn't verify", not broken.
3. **The change itself works as intended.** From the merged PR's description and diff, list
   what should now be true on the live site, then check each one and report pass/fail per item:
   - **Added or changed things** are present on every page they should be on, and they work:
     links reach a live page or video, images load, embeds play.
   - **Removed things** are gone from every page, not just one.
   - **Layout or styling changes** look right: take screenshots with the pre-installed headless
     browser (Playwright/Chromium) at desktop and phone widths and look at them.
   - **Interactive changes** (menus, forms, players) behave correctly when exercised in the
     headless browser.
   - If the PR doesn't change the live site (notes or docs only), say so and confirm the new
     files weren't published by mistake.
