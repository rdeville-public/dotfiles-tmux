<!-- BEGIN DOTGIT-SYNC BLOCK MANAGED -->
<!-- markdownlint-disable -->

# 👋 Welcome to Tmux Config

<center>

> ⚠️ IMPORTANT !
>
> Main repo is on [framagit.org](https://framagit.org/rdeville-public/dotfiles/tmux).
>
> On other online git platforms, they are just mirror of the main repo.
>
> Any issues, pull/merge requests, etc., might not be considered on those other
> platforms.

</center>

---

<center>

[![Licenses: (MIT OR BEERWARE)][license_badge]][license_url]
[![Changelog][changelog_badge]][changelog_badge_url]
[![Build][build_badge]][build_badge_url]
[![Release][release_badge]][release_badge_url]

</center>

[build_badge]: https://framagit.org/rdeville-public/dotfiles/tmux/badges/main/pipeline.svg
[build_badge_url]: https://framagit.org/rdeville-public/dotfiles/tmux/-/commits/main
[release_badge]: https://framagit.org/rdeville-public/dotfiles/tmux/-/badges/release.svg
[release_badge_url]: https://framagit.org/rdeville-public/dotfiles/tmux/-/releases/
[license_badge]: https://img.shields.io/badge/Licenses-MIT%20OR%20BEERWARE-blue
[license_url]: https://framagit.org/rdeville-public/dotfiles/tmux/blob/main/LICENSE
[changelog_badge]: https://img.shields.io/badge/Changelog-Python%20Semantic%20Release-yellow
[changelog_badge_url]: https://github.com/python-semantic-release/python-semantic-release

My generic public tmux configuration which load custom config stored in
~/.local/share/tmux (by default) to store configuration per hosts.

---

<!-- BEGIN DOTGIT-SYNC BLOCK EXCLUDED CUSTOM_README -->
<!-- TODO: @rdeville: Add Asciinema demo one day
## 🎦 Showcase

Sometimes, image worth thousands words. So below is a showcase of this tmux
configuration without customization.

-->

## 📌 Prerequisites

- Tmux: `>= v3.4`
- Python3: `>= 3.10` (for [tmux-fzf-links](https://github.com/alberti42/tmux-fzf-links))

For neovim integration, you should install [nvim-tmux-navigator](https://github.com/alexghergh/nvim-tmux-navigation)
in your Vim/NeoVim configuration.

## ⚙️ Install

### Using Flake and Home-Manager

If you use nix Home-Manager with flake, add the following configuration to your
`flake.nix`:

```nix
{
  inputs = {
    nixpkgs = {
      url = "github:nixos/nixpkgs/nixos-unstable";
    };
    tmuxrc = {
      url = "git+https://framagit.org/rdeville-public/dotfiles/tmux";
      inputs = {
        nixpkgs.follows = "nixpkgs";
      };
    };
  };


  outputs = inputs @ {self, ...}: {
    homeConfigurations = {
      "user@hostname" = inputs.home-manager.lib.homeManagerConfiguration {
        modules = [
          # HM module for this repo
          inputs.tmuxrc.HomeManagerModules.tmuxrc
          # Your other modules here
          [...]
          # Finally, your home.nix here:
          ({...}: {
            tmuxrc = {
              enable = true;
            };
          })
        ];
      };
    };

  };
}
```

### Manually

To use this configuration out-of-the-box, simply clone it in `~/.config/tmux`:

```bash
git clone https://framagit.org/rdeville-public/dotfiles/tmux.git ~/.config/tmux
```

**IMPORTANT**: If you have a file `~/.tmux.conf`, this configuration might not
work.

## 🚀 Usage

Simply run `tmux`, this should load the configuration automagically.

### Keyboard Added Bindings

Below are some of my main keyboard shortcuts.

For personal convenience, I map lots of shortcuts to direct access using `M-x`,
where `x` is the character.

Nevertheless, most of the default Tmux shortcuts are kept and default shortcuts
base on `<prefix>` are still presents. Deactivated shortcuts are listed at the
end of this section.

| Shortcut    | Mode      | Description                                                                                                           |
| :---------- | :-------- | :-------------------------------------------------------------------------------------------------------------------- |
| `C-h`       | Any       | Focus to left pane, integrated with NeoVim/Vim                                                                        |
| `C-j`       | Any       | Focus to bottom pane, integrated with NeoVim/Vim                                                                      |
| `C-k`       | Any       | Focus to top pane, integrated with NeoVim/Vim                                                                         |
| `C-l`       | Any       | Focus to right pane, integrated with NeoVim/Vim                                                                       |
| `M-H`[^1]   | Any       | Increase pane left by 5 block                                                                                         |
| `M-J`[^1]   | Any       | Increase pane down by 5 block                                                                                         |
| `M-K`[^1]   | Any       | Increase pane up by 5 block                                                                                           |
| `M-L`[^1]   | Any       | Increase pane right by 5 block                                                                                        |
| `M-h`       | Any       | Move to previous window                                                                                               |
| `M-l`       | Any       | Move to next window                                                                                                   |
| `M-j`       | Any       | Switch to pane to next index                                                                                          |
| `M-k`       | Any       | Switch to pane to previous index                                                                                      |
| `M-r`       | Any       | Reload tmux configuration                                                                                             |
| `<prefix>c` | Any       | Create new tmux window                                                                                                |
| `M-c`       | Any       | Create new tmux window                                                                                                |
| `M-t`       | Any       | Create new tmux window                                                                                                |
| `<prefix>r` | Any       | Rename current window                                                                                                 |
| `<prefix>R` | Any       | Rename current session                                                                                                |
| `<prefix>v` | Any       | Split window vertically                                                                                               |
| `<prefix>h` | Any       | Split window horizontally                                                                                             |
| `M-x`       | Any       | Kill pane with confirmation                                                                                           |
| `M-w`       | Any       | Kill window with confirmation                                                                                         |
| `M-q`       | Any       | Kill session with confirmation                                                                                        |
| `<prefix>m` | Any       | Toggle on/off pane activity monitoring                                                                                |
| `M-esc`     | Any       | Switch to copy-mode                                                                                                   |
| `M-v`       | Any       | Past last entry from tmux clipboard buffer                                                                            |
| `M-p`       | Any       | Chose entry from tmux clipboard buffer and past it                                                                    |
| `M-i`       | Any       | Start "quake" floating terminal                                                                                       |
| `M-I`       | Any       | Install plugins                                                                                                       |
| `M-r`       | Any       | Reload tmux configuration                                                                                             |
| `M-s`       | Any       | Show FZF session selection menu ((fzf-sessions-switch)[https://github.com/cutbypham/tmux-fzf-session-switch])         |
| `M-f`       | Any       | Start a tmux "finger" to select pattern from current window ((tmux-thumbs)[https://github.com/fcsonline/tmux-thumbs]) |
| `<prefi>u`  | Any       | Show FZF URL selection and open it in your browser ((tmux-fzf-url)[https://github.com/wfxr/tmux-fzf-url])             |
| `<prefi>p`  | Any       | Show FZF URL and file selection ([tmux-fzf-links](https://github.com/alberti42/tmux-fzf-links/))                      |
| `F12`       | Any       | Deactivate/Activate tmux shortcuts[^2]                                                                                |
| `v`         | copy-mode | Begin selection                                                                                                       |
| `V`         | copy-mode | Once in selection, toggle rectangle selection                                                                         |
| `y`         | copy-mode | Copy selection and exit copy-mode                                                                                     |
| `Y`         | copy-mode | Copy line                                                                                                             |

[^1]:
    This is capital letter, implicitly `M-S-x` where `x` is the letter. Your
    terminal emulator should be able to support `Alt` with capital letter.
    Normally, should work with most of the terminal emulator, except for
    Alacritty on MacOS. In this configuration, you may need to update your
    Alacritty configuration as describe in this issue :

    - [alacritty/alacritty#7637](https://github.com/alacritty/alacritty/issues/7637)

[^2]:
    Useful when using Tmux in Tmux. For instance, you are in a Tmux one your
    local computer, then SSH to a server and start a Tmux within your server.
    Instead of using `<prefix><prefi>` to send command to your distant Tmux,
    simply press `F12`. This will deactivate your local Tmux and send shortcuts
    directly to your distant Tmux session.

IMPORTANT ! To use `F12` shortcuts, following lines MUST BE present on both your
local and distant tmux configuration :

```tmux
# SSH toggle nested tmux key binding
# -----------------------------------------------------------------------------
# We want to have single prefix key "prefix", usable both for local and remote session
# we don't want to "prefix" + "a" approach either
# Idea is to turn off all key bindings and prefix handling on local session,
# so that all keystrokes are passed to inner/remote session

# See: toggle on/off all keybindings · Issue #237 · tmux/tmux -
#   https://github.com/tmux/tmux/issues/237

# Also, change some visual styles when window keys are off
bind -T root F12 "
 set prefix None
 set prefix2 None
 set key-table off
 set status-position top
 if -F '#{pane_in_mode}' 'send-keys -X cancel'
 refresh-client -S"

bind -T off F12 "
 set -u prefix
 set -u prefix2
 set -u key-table
 set status-position bottom
 refresh-client -S"

```

### Keyboard Remove Binding

Below are deactivated default Tmux shortcuts since I remapped most of them:

```tmux
# Key Unbindings
# =============================================================================
# Unbind default key bindings, we"re going to override
unbind "\$" # rename-session
unbind ,    # rename-window
unbind %    # split-window -h
unbind '"'  # split-window
unbind "}"  # swap-pane -D
unbind "{"  # swap-pane -U
unbind "["  # copy-moda
unbind "]"  # paste-buffer -P
unbind "'"  # select-window
unbind n    # next-window
unbind p    # previous-window
unbind l    # last-window
unbind M-n  # next window with alert
unbind M-p  # next window with alert
unbind o    # focus thru panes
unbind &    # kill-window
unbind "#"  # list-buffer
unbind =    # choose-buffer
unbind z    # zoom-pane
unbind M-Up  # resize 5 rows up
unbind M-Down # resize 5 rows down
unbind M-Right # resize 5 rows right
unbind M-Left # resize 5 rows left
```

### Custom Configuration

If you want to change colors, you can do it by creating file
`~/.local/share/tmux/tmux.conf` with the following content with your updated
values :

```tmux
# Tmux Systat Plugins (local)
# -----------------------------------------------------------------------------
# Set separator module
set -g @separator_right ""
set -g @separator_left ""
# Set status line colors
set -g @status_bg "#616161"
set -g @status_fg "#f5f5f5"
# Set date
set -g @date_format "%a %d %b | %H:%M"
set -g @date_fg "#ffffff"
set -g @date_bg "#424242"
# Set window
set -g @window_format "#I:#W"
set -g @window_bg "#9e9e9e"
set -g @window_fg "#616161"
set -g @window_current_bg "#bdbdbd"
set -g @window_current_fg "#000000"
# Set pane border colors
set -g @pane_border_fg "#263238"
set -g @pane_border_bg "#263238"
set -g @pane_active_border_fg "#9e9e9e"
set -g @pane_active_border_bg "#263238"
```

<!-- END DOTGIT-SYNC BLOCK EXCLUDED CUSTOM_README -->

## 🤝 Contributing

Contributions, issues and feature requests are welcome!

Feel free to check [issues page][issues_pages].

You can also take a look at the [CONTRIBUTING.md][contributing].

[issues_pages]: https://framagit.org/rdeville-public/dotfiles/tmux/-/issues
[contributing]: https://framagit.org/rdeville-public/dotfiles/tmux/blob/main/CONTRIBUTING.md

## 👤 Maintainers

- 📧 [**Romain Deville** \<code@romaindeville.fr\>](mailto:code@romaindeville.fr)
  - Website: [https://romaindeville.fr](https://romaindeville.fr)
  - Github: [@rdeville](https://github.com/rdeville)
  - Gitlab: [@r.deville](https://gitlab.com/r.deville)
  - Framagit: [@rdeville](https://framagit.org/rdeville)

## 📝 License

Copyright © 2022 - 2025

- [Romain Deville \<code@romaindeville.fr\>](code@romaindeville.fr)

This project is under following licenses (**OR**) :

- [MIT][main_license]
- [BEERWARE][beerware_license]

[main_license]: https://framagit.org/rdeville-public/dotfiles/tmux/blob/main/LICENSE
[beerware_license]: https://framagit.org/rdeville-public/dotfiles/tmux/blob/main/LICENSE.BEERWARE

<!-- END DOTGIT-SYNC BLOCK MANAGED -->
