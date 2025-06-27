# drun-frecency
App launcher powered by frecency

## Motivation
I wanted an app launcher meeting the following criteria:
1. Frecency-based sorting
2. Use any kind of menu, like "dmenu", "bemenu", "rofi -dmenu"
3. Works with flatpak entries
4. Filter either through the name of generic name
5. Hackable

## Frecency
The word "frecency" itself is a combination of the words "frequency" and "recency."

For every entry's frecency score calculation, two things happen:
1. A ratio ranging from 0 to 1 is calculated.
   - The ratio will be closer to 1 if you launched it recently, or 0 if you didn't launched that app in the past 90 days (configurable).
2. The last frecency score is then multiplied by this ratio and applied to the entry

Every time you launch an application, it's frecency is updated and it receives 100 points.

Inspired by [Mozilla: Frecency algorithm](https://web.archive.org/web/20210421120120/https://developer.mozilla.org/en-US/docs/Mozilla/Tech/Places/Frecency_algorithm) and many other tools already incorporating frecency algorithms like [telescope-frecency](https://github.com/nvim-telescope/telescope-frecency.nvim/blob/master/README.md)
