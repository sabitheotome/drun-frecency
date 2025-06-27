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

## Environment variables

| Variable                 | Description                                                                          | Value              | Default                             | Obs.                                                                                      |
| ------------------------ | ------------------------------------------------------------------------------------ | ------------------ | ----------------------------------- | ----------------------------------------------------------------------------------------- |
| DRUN_DMENU or DMENU      | Menu program                                                                         | Shell command      | `dmenu`                             | DRUN_DMENU takes priority over DMENU                                                      |
| DRUN_OPENER              | Launcher program for .desktop files                                                  | Shell command      |                                     | Falls back to `dex`, `gio launch`, `gtk-launch`, `kde-open`, and `xdg-open`               |
| DRUN_FRECENCY_THRESHOLD  | The time it takes for the score to approach zero since the last time it was launched | Integer in seconds | 7776000                             | 90 days by default                                                                        |
| DRUN_FRECENCY_WEIGHT     | Value added to the score for each launch                                             | Integer            | 100                                 |                                                                                           |
| DRUN_FRECENCY_CACHE_FILE | File hosting the frecency table                                                      | File path          | `$XDG_CACHE_HOME`/drun-frecency.txt | Does not create parent directories. `$HOME`/.cache is used if `$XDG_CACHE_HOME` is empty. |
| DRUN_ENTRIES_CACHE_FILE  | File containing all sorted and formatted entries' names                              | File path          | `$XDG_CACHE_HOME`/drun-entries.txt  | Does not create parent directories. `$HOME`/.cache is used if `$XDG_CACHE_HOME` is empty. |
| DRUN_INDEX_CACHE_FILE    | File containing all entries' paths                                                   | File path          | `$XDG_CACHE_HOME`/drun-index.txt    | Does not create parent directories. `$HOME`/.cache is used if `$XDG_CACHE_HOME` is empty. |

## Inspiration

Inspired by [Mozilla: Frecency algorithm](https://web.archive.org/web/20210421120120/https://developer.mozilla.org/en-US/docs/Mozilla/Tech/Places/Frecency_algorithm) and many other tools already incorporating frecency algorithms like [telescope-frecency](https://github.com/nvim-telescope/telescope-frecency.nvim/blob/master/README.md)
