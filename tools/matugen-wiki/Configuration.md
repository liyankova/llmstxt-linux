# Creating templates

## Keywords
> [!IMPORTANT]
> Since 1.0.0, you have to define the scheme and format instead of leaving both empty for default values.

- Basic syntax: `{{<key>}}`
- Colors: `{{colors.<color>.<scheme>.<format>}}`
- Image: `{{image}}`
- Custom: `{{custom.<keyword>}}`

## Colors
<img src="https://github.com/InioX/matugen/assets/81521595/de03487e-211f-4135-a23f-38f55f3fd7b3" height=50% width=50%>

`A` - All colors start with the `{{colors.` prefix

`B` - The color keyword from [here](example-of-all-the-color-keywords)

`C` - The scheme (light, dark or `default`)

`D` - The format from [here](#Example-of-all-the-formats)

### Example of all the color keywords:
| Keyword                    	| Keyword                       |
|----------------------------	|----------------------------	|
| primary                    	|error                      	|
| on_primary                 	|on_error                   	|
| primary_container          	|error_container            	|
| on_primary_container       	|on_error_container         	|
| inverse_primary            	|surface_dim                	|
| primary_fixed              	|surface                    	|
| primary_fixed_dim          	|surface_bright             	|
| on_primary_fixed           	|surface_container_lowest   	|
| on_primary_fixed_variant   	|surface_container_low      	|
| secondary                  	|surface_container          	|
| on_secondary               	|surface_container_high     	|
| secondary_container        	|surface_container_highest  	|
| on_secondary_container     	|on_surface                 	|
| secondary_fixed            	|on_surface_variant         	|
| secondary_fixed_dim        	|outline                    	|
| on_secondary_fixed         	|outline_variant            	|
| on_secondary_fixed_variant 	|inverse_surface            	|
| tertiary                   	|inverse_on_surface         	|
| on_tertiary                	|surface_variant            	|
| tertiary_container         	|background                 	|
| on_tertiary_container      	|on_background              	|
| tertiary_fixed             	|shadow                     	|
| tertiary_fixed_dim         	|scrim                      	|
| on_tertiary_fixed          	|on_tertiary_fixed_variant  	
| source_color  	|

<img src="https://github.com/InioX/matugen/assets/81521595/4d8c7caf-b99d-41f5-9d9e-fbe7099029b5" height=50% width=50%>

### Example of all the formats:

| Format       	| Example Output             	|
|--------------	|----------------------------	|
| hex          	| `#ffffff`                  	|
| hex_stripped 	| `ffffff`                   	|
| rgb          	| `rgb(255, 255, 255)`       	|
| rgba         	| `rgba(255, 255, 255, 255)` 	|
| hsl          	| `hsl(0, 0%, 0%)`           	|
| hsla         	| `hsla(0, 0%, 0%, 0.0)`     	|
| red          	| `255`                      	|
| green        	| `255`                      	|
| blue         	| `255`                      	|
| alpha        	| `255`                      	|
| hue          	| `255`                      	|
| saturation   	| `255`                      	|
| lightness    	| `255`                      	|

### Image
You can also get the image path (if it was provided) by using:
```
{{image}}
```

### Custom keywords
Example config:
```toml
[config.custom_keywords]
font1 = "Google Sans"
```
Usage in templates:
```
{{ custom.font1 }}
```

### Custom colors
Example config:
```toml
[config.custom_colors]
red = { color = "#ff0000", blend = false }
```
Usage in templates:
```
{{ colors.red.default.hex }}
```

# Configuration
Here is a list of different locations for the configuration file:
- Windows: `C:\Users\user\AppData\Roaming\InioX\matugen\config\config.toml`
- Linux: `/home/user/.config/matugen/config.toml`
- MacOS: `/Users/user/Library/Application Support/com.InioX.matugen/config.toml`

> [!TIP]
> You can also use a custom configuration path by using the `-c` argument

### Example
[Check the example configuration here](https://github.com/InioX/matugen/blob/main/example/config.toml)

### Configuring wallpaper
Wallpaper configuration can be set under `[config.wallpaper]`
| Name        | Type                  | Default   | Description                                                                            |
|-------------|-----------------------|-----------|----------------------------------------------------------------------------------------|
| set         | bool                  | true      | Setting this to false will skip setting wallpaper.                                     |
| pre_hook    | Option\<String\>        | None      | Runs before setting wallpaper. Useful for, for example, killing the wallpaper daemon.  |
| command     | String                | None      | Command used for setting wallpaper.                                                    |
| arguments   | Option\<Vec\<String\>\>   | None      | Arguments to pass to the wallpaper command. The last argument will be the image path.  |

#### Example
```toml
# config_directory/config.toml
[config.wallpaper]
command = "swww"
arguments = ["img", "--transition-type", "center"]
set = true
# pre_hook = ""
```

### Adding templates
| Name            | Type                  | Default                   | Description                             |
|-----------------|-----------------------|---------------------------|-----------------------------------------|
| ~~mode~~            | ~~Option\<Modes\>~~       | ~~Mode provided in args~~     | ~~Which scheme to use for the template.~~   |
| input_path      | PathBuf               | None                      | Path to the template file.              |
| output_path     | PathBuf               | None                      | Path to export the template to.         |

#### Example
```toml
# config_directory/config.toml

[templates.test] # First way of adding template
input_path = '~/.config/example/template.css'
output_path = '~/.config/example'

[templates] # Another way
test2 = { input_path = '~/.config/example/template2.css', output_path = '~/.config/example2' }
```