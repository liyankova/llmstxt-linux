<div align="center">
     <img src="https://github.com/InioX/matugen/assets/81521595/66cfec75-702c-4b55-83fc-c474de171057" width=55% height=55%>
     <br><br>
     <img src="https://github.com/InioX/matugen/assets/81521595/ec3a165d-442d-4494-9aec-24254d11ae61" width=50% height=50%>
</div>

<div align="center">
  <img src="https://github.com/InioX/matugen/assets/81521595/9008d8d9-0157-4b38-9500-597986a2cb9f">
</div>

## Contents
- [Configuration](wiki/Configuration) - Shows information about configuration and creating templates
- [Configuration before 1.0.0](wiki/Configuration-before-1.0.0) - Same as `Configuration` but for the old version.
- [Filters](wiki/Filters) - Shows usage and examples of using filters in templates 
- [Usage](wiki/Usage) - Shows usage in the CLI 
- [Templates](wiki/Templates) - Additional advanced syntax for templates
- [Templates Before 3.0.0](wiki/Templates-Before-3.0.0) - Additional advanced syntax for templates
- [Features](wiki/Features) - Shows how to compile Matugen with features, and which features there are.

## Basics

The best way to get started is to look at the official template [theme repo](https://github.com/InioX/matugen-themes)

Running `matugen image <image_path>` will "compile" all the templates configured in the `[templates]` section of `$HOME/.config/matugen/config.toml`.
You can do this to get started (assuming you use [swww](https://github.com/Horus645/swww) and it's in matugen's `$PATH`)

#### 1. Write the following to that `config.toml` file
```toml
[config.wallpaper]
command = "swww"
arguments = ["img", "--transition-type", "center"]
set = true


[templates.waybar]
input_path = './templates/colors.css'
output_path = '~/.config/waybar/colors.css'
post_hook = 'pkill -SIGUSR2 waybar'
```

#### 2. Copy [colors.css](https://github.com/iniox/matugen-themes/blob/main/templates/colors.css) to `$HOME/.config/matugen/templates/colors.css`

#### 3. Add this line to the top of your `~/.config/waybar/style.css` file
```css
@import "colors.css";
```

#### 4. Run `matugen image <whatever_wallpaper_you_want>`