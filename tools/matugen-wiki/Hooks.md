# Hooks

You can use hooks inside the `[templates]` section of the `config.toml` file and also in `[config.wallpaper.pre_hook]`

- `pre_hook`: Executes a command inside the string BEFORE the template is generated
- `post_hook`: Executes a command inside the string AFTER the template is generated

#### Example hook usage

```
[templates.test]
input_path = "some/path"
output_path = "some/path"
pre_hook = 'echo "hello world"'
post_hook = "cat /some/file.txt"
```