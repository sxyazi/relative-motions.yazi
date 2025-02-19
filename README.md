# relative-motions.yazi

A [Yazi](https://github.com/sxyazi/yazi) plugin based about vim motions.

> [!NOTE]
> The latest main branch of Yazi is required at the moment.

https://github.com/dedukun/relative-motions.yazi/assets/25795432/04fb186a-5efe-442d-8d7b-2dccb6eee408

## Installation

```sh
# Linux/macOS
git clone https://github.com/dedukun/relative-motions.yazi.git ~/.config/yazi/plugins/relative-motions.yazi

# Windows
git clone https://github.com/dedukun/relative-motions.yazi.git %AppData%\yazi\config\plugins\relative-motions.yazi
```

## Configuration

If you want to use the numbers directly to start a motion add this to your `keymap.toml`:

<details>

```toml
[[manager.prepend_keymap]]
on = [ "1" ]
exec = "plugin relative-motions --args=1"
desc = "Move in relative steps"

[[manager.prepend_keymap]]
on = [ "2" ]
exec = "plugin relative-motions --args=2"
desc = "Move in relative steps"

[[manager.prepend_keymap]]
on = [ "3" ]
exec = "plugin relative-motions --args=3"
desc = "Move in relative steps"

[[manager.prepend_keymap]]
on = [ "4" ]
exec = "plugin relative-motions --args=4"
desc = "Move in relative steps"

[[manager.prepend_keymap]]
on = [ "5" ]
exec = "plugin relative-motions --args=5"
desc = "Move in relative steps"

[[manager.prepend_keymap]]
on = [ "6" ]
exec = "plugin relative-motions --args=6"
desc = "Move in relative steps"

[[manager.prepend_keymap]]
on = [ "7" ]
exec = "plugin relative-motions --args=7"
desc = "Move in relative steps"

[[manager.prepend_keymap]]
on = [ "8" ]
exec = "plugin relative-motions --args=8"
desc = "Move in relative steps"

[[manager.prepend_keymap]]
on = [ "9" ]
exec = "plugin relative-motions --args=9"
desc = "Move in relative steps"
```

</details>

Alternatively you can use a key to trigger a new motion without any initial value, for that add the following in `keymap.toml`:

```toml
[[manager.prepend_keymap]]
on = [ "m" ]
exec = "plugin relative-motions"
desc = "Trigger a new relative motion"
```

---

Additionally there are a couple of initial configurations that can be given to the plugin's `setup` function:

| Configuration  | Values                                                | Default | Description                                                                                                                        |
| -------------- | ----------------------------------------------------- | ------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| `show_numbers` | `relative`, `absolute`, `relative_absolute` or `none` | `none`  | Shows relative or absolute numbers before the file icon                                                                            |
| `show_motion`  | `true` or `false`                                     | `false` | Shows current motion in Status bar                                                                                                 |
| `only_motions` | `true` or `false`                                     | `false` | If true, only the motion movements will be enabled, i.e., the commands for delete, cut, yank and visual selection will be disabled |

If you want, for exemple, to enable relative numbers as well as to show the motion in the status bar,
add the following to `init.lua`:

```lua
require("relative-motions"):setup({ show_numbers="relative", show_motion = true })
```

> [!NOTE]
> The `show_numbers` and `show_motion` functionalities overwrite [`Current:render`](https://github.com/sxyazi/yazi/blob/e51e8ad789914b2ab4a9485da7aa7fbc7b3bb450/yazi-plugin/preset/components/current.lua#L5)
> and [`Status:render`](https://github.com/sxyazi/yazi/blob/e51e8ad789914b2ab4a9485da7aa7fbc7b3bb450/yazi-plugin/preset/components/status.lua#L111) respectively.
> If you have custom implementations for any of this functions
> you can add the provided `File:number` and `Status:motion` to your implementations, just check [here](https://github.com/dedukun/relative-motions.yazi/blob/main/init.lua#L39) how we are doing things.

## Usage

This plugin adds the some basic vim motions like `3k`, `12j`, `10gg`, etc.
The following table show all the available motions:

| Command | Description         |
| ------- | ------------------- |
| `j`     | Move `n` lines down |
| `k`     | Move `n` lines up   |
| `gj`    | Go `n` lines down   |
| `gk`    | Go `n` lines up     |
| `gg`    | Go to line          |

Furthermore, the following operations were also added:

| Command | Description   |
| ------- | ------------- |
| `v`     | visual select |
| `y`     | Yank          |
| `x`     | Cut           |
| `d`     | Delete motion |

This however must be followed by a direction, which can be `j`, `k` or repeating the command key,
which will operate from the cursor down, e.g. `2yy` will copy two files.
