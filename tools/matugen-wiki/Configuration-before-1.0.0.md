### Creating templates
The basic syntax for using colors is `prefix + {color}` (The default prefix is `@`, so the usage would be `@{color}`).

#### Keywords
If you want a specific scheme, you can use `@{primary.light.hex}`. All available modes/schemes can be found <a href="#usage">here</a>.

```css
@define-color primary @{primary}; /* Result: #ffb783 */
@define-color primary @{primary.hex}; /* Result: #ffb783 */
@define-color primary @{primary.rgb}; /* Result: rgb(255, 183, 131) */
@define-color primary @{primary.rgba}; /* Result: rgba(255, 183, 131, 255) */
@define-color primary @{primary.strip}; /* Result: ffb783 */
@define-color primary @{primary.hsl}; /* Result: hsl(25, 100%, 76%) */
@define-color primary @{primary.hsla}; /* Result: hsla(242.2, 49.4%, 67.45%, 1) */

@define-color primary @{background.light.hex}; /* Result: #fffbff */
@define-color primary @{background.dark.hex}; /* Result: #1e1b19 */
@define-color primary @{background.amoled.hex}; /* Result: #000000 */
```

You can get the source color (color used for generating colorscheme) by using:
```css
@import url("@{source_color}"); /* Result: #ffb783*/
```

You can also get the image (if it was provided) by using:
```css
@import url("@{image}"); /* Result: /home/ini/Downloads/wallpaper.jpg */
```
> **Note**
> If no image was provided, Matugen will just skip over the image keyword

#### Example of all the color keywords:
```css
@define-color source_color @{source_color};
@define-color primary @{primary};
@define-color primary_fixed @{primary_fixed};
@define-color primary_fixed_dim @{primary_fixed_dim};
@define-color on_primary @{on_primary};
@define-color on_primary_fixed @{on_primary_fixed};
@define-color on_primary_fixed_variant @{on_primary_fixed_variant};
@define-color primary_container @{primary_container};
@define-color on_primary_container @{on_primary_container};
@define-color secondary @{secondary};
@define-color secondary_fixed @{secondary_fixed};
@define-color secondary_fixed_dim @{secondary_fixed_dim};
@define-color on_secondary @{on_secondary};
@define-color on_secondary_fixed @{on_secondary_fixed};
@define-color on_secondary_fixed_variant @{on_secondary_fixed_variant};
@define-color secondary_container @{secondary_container};
@define-color on_secondary_container @{on_secondary_container};
@define-color tertiary @{tertiary};
@define-color tertiary_fixed @{tertiary_fixed};
@define-color tertiary_fixed_dim @{tertiary_fixed_dim};
@define-color on_tertiary @{on_tertiary};
@define-color on_tertiary_fixed @{on_tertiary_fixed};
@define-color on_tertiary_fixed_variant @{on_tertiary_fixed_variant};
@define-color tertiary_container @{tertiary_container};
@define-color on_tertiary_container @{on_tertiary_container};
@define-color error @{error};
@define-color on_error @{on_error};
@define-color error_container @{error_container};
@define-color on_error_container @{on_error_container};
@define-color surface @{surface};
@define-color on_surface @{on_surface};
@define-color on_surface_variant @{on_surface_variant};
@define-color outline @{outline};
@define-color outline_variant @{outline_variant};
@define-color shadow @{shadow};
@define-color scrim @{scrim};
@define-color inverse_surface @{inverse_surface};
@define-color inverse_on_surface @{inverse_on_surface};
@define-color inverse_primary @{inverse_primary};
@define-color surface_dim @{surface_dim};
@define-color surface_bright @{surface_bright};
@define-color surface_container_lowest @{surface_container_lowest};
@define-color surface_container_low @{surface_container_low};
@define-color surface_container @{surface_container};
@define-color surface_container_high @{surface_container_high};
@define-color surface_container_highest @{surface_container_highest};

@define-color source_color @{source_color};
@define-color color_accent_primary @{color_accent_primary};
@define-color color_accent_primary_variant @{color_accent_primary_variant};
@define-color color_accent_secondary @{color_accent_secondary};
@define-color color_accent_secondary_variant @{color_accent_secondary_variant};
@define-color color_accent_tertiary @{color_accent_tertiary};
@define-color color_accent_tertiary_variant @{color_accent_tertiary_variant};
@define-color text_color_primary @{text_color_primary};
@define-color text_color_secondary @{text_color_secondary};
@define-color text_color_tertiary @{text_color_tertiary};
@define-color text_color_primary_inverse @{text_color_primary_inverse};
@define-color text_color_secondary_inverse @{text_color_secondary_inverse};
@define-color text_color_tertiary_inverse @{text_color_tertiary_inverse};
@define-color color_background @{color_background};
@define-color color_background_floating @{color_background_floating};
@define-color color_surface @{color_surface};
@define-color color_surface_variant @{color_surface_variant};
@define-color color_surface_highlight @{color_surface_highlight};
@define-color surface_header @{surface_header};
@define-color under_surface @{under_surface};
@define-color off_state @{off_state};
@define-color accent_surface @{accent_surface};
@define-color text_primary_on_accent @{text_primary_on_accent};
@define-color text_secondary_on_accent @{text_secondary_on_accent};
@define-color volume_background @{volume_background};
@define-color scrim_android @{scrim_android};
```

## Configuration
Here is a list of different locations for the configuration file:
- Windows: `C:\Users\user\AppData\Roaming\InioX\matugen\config\config.toml`
- Linux: `/home/user/.config/matugen/config.toml`
- MacOS: `/Users/user/Library/Application Support/com.InioX.matugen/config.toml`

> [!TIP]
> You can also use a custom configuration path by using the `-c` argument

### Configuration items
| Name                 | Type          | Default   | Description                                                                                     |
|----------------------|---------------|-----------|-------------------------------------------------------------------------------------------------|
| reload_apps          | bool          | false     | Whether to reload apps.                                                                         |
| set_wallpaper        | bool          | false     | Whether to set the wallpaper (if `true`, requires `wallpaper_tool` to be set).                  |
| wallpaper_tool       | String        | None      | The wallpaper tool to use (`Swwww`, `Swaybg`, `Feh`, `Nitrogen`).                               |
| prefix               | String        | "@"       | The prefix to use (for example: `@{primary}`)                                                   |
| ~~reload_gtk_theme~~ | ~~bool~~      | ~~false~~ | ~~Whether to reload the gtk theme.~~ **REMOVED, USE `gtk_theme` in `config.reload_apps_list`.** |
| ~run_after~            | ~Vec<String>~   | ~[]~        | ~The commands to run after the templates have been generated.~ **REMOVED, USE A WRAPPER FUNCTION FOR MATUGEN INSTEAD.**                                 |
| swww_options         | <Vec<String>> | []        | The options to use for [Swwww](https://github.com/Horus645/swww)                                |
| feh_options          | <Vec<String>> | []        | The options to use for [Feh](https://github.com/derf/feh)                                       |

### Apps
| Name      | Type | Default | Description                      |
|-----------|------|---------|----------------------------------|
| kitty     | bool | true    | Whether to reload kitty.         |
| waybar    | bool | true    | Whether to reload waybar.        |
| dunst     | bool | true    | Whether to reload dunst.         |
| gtk_theme | bool | true    | Whether to reload the GTK theme. |

### Example
```toml
# config_directory/config.toml
[config]
reload_apps = true
set_wallpaper = true
wallpaper_tool = 'Swww'
prefix = '@'
swww_options = [
    "--transition-type",
    "center",
]
run_after = [
    [ "echo", "'hello'" ],
    [ "echo", "'hello again'" ],
]

[config.reload_apps_list]
waybar = true
kitty = true
gtk_theme = true
dunst = true
```

### Adding templates
| Name            | Type                  | Default                   | Description                             |
|-----------------|-----------------------|---------------------------|-----------------------------------------|
| mode            | Option\<Modes\>       | Mode provided in args     | Which scheme to use for the template.   |
| input_path      | PathBuf               | None                      | Path to the template file.              |
| output_path     | PathBuf               | None                      | Path to export the template to.         |

### Modes
> [!NOTE]
> The `mode` key will override the mode specified in the arguments, only for that template.

For all available modes, look at the <a href="#usage">usage</a>.

### Example
```toml
# config_directory/config.toml

[templates.test] # First way of adding template
input_path = '~/.config/example/template.css'
output_path = '~/.config/example'
mode = "Light" # First letter MUST be upper-case

[templates] # Another way
test2 = { input_path = '~/.config/example/template2.css', output_path = '~/.config/example2' }
```