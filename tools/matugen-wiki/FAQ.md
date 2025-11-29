# FAQ

## How do I use matugen colors with the hyprland config format?

- Without:
```
general {
    col.inactive_border = rgb({{colors.background.default.hex_stripped}})
    col.active_border = rgb({{colors.primary.default.hex_stripped}})
}
```

- With alpha:

```
general {
    col.inactive_border = rgba({{colors.background.default.hex_stripped}}77)
    col.active_border = rgba({{colors.primary.default.hex_stripped}}44)
}
```