### Modes
<img src="./assets/images/modes.gif" width=450>

<table>
<tr>
    <td>Light</td>
    <td>Dark</td>
  </tr>
    <tr>
    <td><img src="https://media.discordapp.net/attachments/1134177615964545024/1140270597381832774/image.png"></td>
    <td><img src="https://media.discordapp.net/attachments/1134177615964545024/1140270155205713920/image.png"></td>
  </tr>
</table>

### Types
<img src="./assets/images/palette.gif" width=450>


- List of all types:  
  - scheme-content
  - scheme-expressive
  - scheme-fidelity
  - scheme-fruit-salad
  - scheme-monochrome
  - scheme-neutral
  - scheme-rainbow
  - scheme-tonal-spot

### Json flag
Allows for dumping the schemes similarly to `--show-colors`, but in a
machine-readable format. Can dump hex, rgba, hsl, etc.

<details><summary>Result</summary>
<p>

```sh
matugen image <image> --json hex
```

```json
{
  "colors": {
    "amoled": {
      "background": "#000000",
      "error": "#ffb4ab",
      "error_container": "#93000a",
      "inverse_on_surface": "#303033",
      "inverse_primary": "#005ac1",
      "inverse_surface": "#e3e2e6",
      "on_background": "#e3e2e6",
      "on_error": "#690005",
      "on_error_container": "#ffb4ab",
      "on_primary": "#002e69",
      "on_primary_container": "#d8e2ff",
      "on_secondary": "#253048",
      "on_secondary_container": "#d8e2ff",
      "on_surface": "#e3e2e6",
      "on_surface_variant": "#c4c6d0",
      "on_tertiary": "#44244a",
      "on_tertiary_container": "#fed6ff",
      "outline": "#8e9099",
      "outline_variant": "#44474f",
      "primary": "#adc6ff",
      "primary_container": "#004494",
      "scrim": "#000000",
      "secondary": "#bbc6e4",
      "secondary_container": "#3b475f",
      "shadow": "#000000",
      "source_color": "#4285f4",
      "surface": "#000000",
      "surface_variant": "#0e1118",
      "tertiary": "#e5b8e8",
      "tertiary_container": "#5d3a62"
    },
    "dark": {
      "background": "#1b1b1f",
      "error": "#ffb4ab",
      "error_container": "#93000a",
      "inverse_on_surface": "#303033",
      "inverse_primary": "#005ac1",
      "inverse_surface": "#e3e2e6",
      "on_background": "#e3e2e6",
      "on_error": "#690005",
      "on_error_container": "#ffb4ab",
      "on_primary": "#002e69",
      "on_primary_container": "#d8e2ff",
      "on_secondary": "#253048",
      "on_secondary_container": "#d8e2ff",
      "on_surface": "#e3e2e6",
      "on_surface_variant": "#c4c6d0",
      "on_tertiary": "#44244a",
      "on_tertiary_container": "#fed6ff",
      "outline": "#8e9099",
      "outline_variant": "#44474f",
      "primary": "#adc6ff",
      "primary_container": "#004494",
      "scrim": "#000000",
      "secondary": "#bbc6e4",
      "secondary_container": "#3b475f",
      "shadow": "#000000",
      "source_color": "#4285f4",
      "surface": "#1b1b1f",
      "surface_variant": "#44474f",
      "tertiary": "#e5b8e8",
      "tertiary_container": "#5d3a62"
    },
    "light": {
      "background": "#fefbff",
      "error": "#ba1a1a",
      "error_container": "#ffdad6",
      "inverse_on_surface": "#f2f0f4",
      "inverse_primary": "#adc6ff",
      "inverse_surface": "#303033",
      "on_background": "#1b1b1f",
      "on_error": "#ffffff",
      "on_error_container": "#410002",
      "on_primary": "#ffffff",
      "on_primary_container": "#001a41",
      "on_secondary": "#ffffff",
      "on_secondary_container": "#0f1b32",
      "on_surface": "#1b1b1f",
      "on_surface_variant": "#44474f",
      "on_tertiary": "#ffffff",
      "on_tertiary_container": "#2d0e34",
      "outline": "#74777f",
      "outline_variant": "#c4c6d0",
      "primary": "#005ac1",
      "primary_container": "#d8e2ff",
      "scrim": "#000000",
      "secondary": "#535e78",
      "secondary_container": "#d8e2ff",
      "shadow": "#000000",
      "source_color": "#4285f4",
      "surface": "#fefbff",
      "surface_variant": "#e1e2ec",
      "tertiary": "#76517b",
      "tertiary_container": "#fed6ff"
    }
  },
  "colors_android": {
    "amoled": {
      "accent_surface": "#edf0ff",
      "color_accent_primary": "#d8e2ff",
      "color_accent_primary_variant": "#80aaff",
      "color_accent_secondary": "#d8e2ff",
      "color_accent_secondary_variant": "#a0abc8",
      "color_accent_tertiary": "#fed6ff",
      "color_accent_tertiary_variant": "#c89dcb",
      "color_background": "#000000",
      "color_background_floating": "#000000",
      "color_surface": "#101114",
      "color_surface_highlight": "#1b1b1f",
      "color_surface_variant": "#252629",
      "off_state": "#303033",
      "scrim_android": "#c7c6ca",
      "source_color": "#4285f4",
      "surface_header": "#1b1b1f",
      "text_color_primary": "#f2f0f4",
      "text_color_primary_inverse": "#1b1b1f",
      "text_color_secondary": "#c4c6d0",
      "text_color_secondary_inverse": "#46464a",
      "text_color_tertiary": "#8e9099",
      "text_color_tertiary_inverse": "#77777a",
      "text_primary_on_accent": "#1b1b1f",
      "text_secondary_on_accent": "#44474f",
      "under_surface": "#000000",
      "volume_background": "#000000"
    },
    "dark": {
      "accent_surface": "#edf0ff",
      "color_accent_primary": "#d8e2ff",
      "color_accent_primary_variant": "#80aaff",
      "color_accent_secondary": "#d8e2ff",
      "color_accent_secondary_variant": "#a0abc8",
      "color_accent_tertiary": "#fed6ff",
      "color_accent_tertiary_variant": "#c89dcb",
      "color_background": "#1b1b1f",
      "color_background_floating": "#1b1b1f",
      "color_surface": "#303033",
      "color_surface_highlight": "#525256",
      "color_surface_variant": "#46464a",
      "off_state": "#303033",
      "scrim_android": "#c7c6ca",
      "source_color": "#4285f4",
      "surface_header": "#46464a",
      "text_color_primary": "#f2f0f4",
      "text_color_primary_inverse": "#1b1b1f",
      "text_color_secondary": "#c4c6d0",
      "text_color_secondary_inverse": "#46464a",
      "text_color_tertiary": "#8e9099",
      "text_color_tertiary_inverse": "#77777a",
      "text_primary_on_accent": "#1b1b1f",
      "text_secondary_on_accent": "#44474f",
      "under_surface": "#000000",
      "volume_background": "#3b3b3f"
    },
    "light": {
      "accent_surface": "#edf0ff",
      "color_accent_primary": "#d8e2ff",
      "color_accent_primary_variant": "#005ac1",
      "color_accent_secondary": "#d8e2ff",
      "color_accent_secondary_variant": "#535e78",
      "color_accent_tertiary": "#fed6ff",
      "color_accent_tertiary_variant": "#76517b",
      "color_background": "#f2f0f4",
      "color_background_floating": "#faf9fd",
      "color_surface": "#faf9fd",
      "color_surface_highlight": "#ffffff",
      "color_surface_variant": "#e3e2e6",
      "off_state": "#303033",
      "scrim_android": "#c7c6ca",
      "source_color": "#4285f4",
      "surface_header": "#e3e2e6",
      "text_color_primary": "#1b1b1f",
      "text_color_primary_inverse": "#f2f0f4",
      "text_color_secondary": "#44474f",
      "text_color_secondary_inverse": "#c7c6ca",
      "text_color_tertiary": "#74777f",
      "text_color_tertiary_inverse": "#919094",
      "text_primary_on_accent": "#1b1b1f",
      "text_secondary_on_accent": "#44474f",
      "under_surface": "#000000",
      "volume_background": "#3b3b3f"
    }
  }
}
```
     
</p>
</details>

```sh
matugen --json <JSON> <other-arguments>
```

### Help
<img src="https://github.com/InioX/matugen/blob/main/assets/images/help.gif" width=450>

```sh
matugen -h
matugen --help
```

### Show colors
<img src="https://media.discordapp.net/attachments/1134177615964545024/1140373989294874764/image.png?width=837&height=684" width=300>

```sh
matugen --show-colors <other-arguments>
```

### Verbose mode
<img src="https://github.com/InioX/matugen/blob/main/assets/images/verbose.gif" width=450>

```sh
matugen -v <other-arguments>
```
     
### Generate from an image
<img src="https://github.com/InioX/matugen/blob/main/assets/images/image.gif" width=450>

```sh
# Dark mode
matugen image /path/to/wallpaper/ -m "dark"
# Light mode
matugen image /path/to/wallpaper/ -m "light"
```
Example:
```sh
matugen image ~/wall/snow.png -l
```

#### Web Image
> [!WARNING]
> Using this will not:
> - Set the wallpaper
> - Replace the {{image}} keyword
> 
> The above might be implemented in the future.

Same as image, but it fetches the image from web.

```sh
matugen web-image <url>
```
     
### Generate from a color
<img src="https://github.com/InioX/matugen/blob/main/assets/images/color.gif" width=450>

```sh
# Dark mode
matugen color hsl <hsl color> -m "dark"
# Light mode
matugen color hex <hex color> -m "light"
```
Example:
```sh
matugen color hex "#ffbf9b"
matugen color rgb "rgb(63, 106, 171)" -m "light"
matugen color hsl "hsl(216.34, 45.75%, 45.88%)" -m "dark"
```