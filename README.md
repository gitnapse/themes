# GitNapse Themes

Public theme registry for [GitNapse](https://github.com/gitnapse/gitnapse).

## Structure

```
themes/
  index.json          # Registry API: machine-readable theme manifest
  colors/             # the themes, one file each
    X.jsonc
    Madrid.jsonc
    ...
  README.md
```

`index.json` is the registry "API": the app queries it to list and search
themes, and uses the `file` paths to download them from `raw.githubusercontent.com`
(no auth needed, public repo).

## Theme format

Colors in hex `#RRGGBB` or RGB `[r, g, b]`:

```jsonc
{
    "theme_name": "X",
    "background": "#050505",   // background color
    "foreground": "#f7f1ff",   // font color (legible against the background)
    "accent": "#fc618d",       // primary accent (selection / focus)
    "accent2": "#7bd88f",      // secondary accent
    "accent3": "#5ad4e6",      // tertiary accent
    "selection_fg": "#000000"  // font on accent backgrounds (optional)
}
```

Legibility rules enforced: `foreground` vs `background` meet **WCAG AA
(contrast ≥ 4.5)**; `selection_fg` is chosen for contrast (omitted when the
accents mix light and dark tones and the app decides per index).

## Use from gitnapse

```sh
gitnapse theme list                 # installed themes (local)
gitnapse theme list --remote        # + themes available in the registry
gitnapse theme install Madrid       # download and install from the registry
gitnapse theme uninstall Madrid     # remove an installed theme
```

Installed themes are stored in `~/.config/GitNapse/themes/`. Select one with
`theme_name` in `theme.jsonc` or from the app's theme picker.

## Contributing a theme

1. Create `colors/<Name>.jsonc` with the format above.
2. Add its entry to `index.json` (name, file, description, dark, background, foreground).
3. Verify legibility: `foreground`/`background` contrast ≥ 4.5.
