# Dotfiles

My configuration files and user preferences.

## License

Generally, it is considered that the content of the dotfiles is governed by the terms and conditions of the software licenses to which they belong. Third-party material under `local/` is credited in [Third-party assets and attribution](#third-party-assets-and-attribution).

## History

Back in 1995, when I first started using Linux, it wasn’t common to back up configuration files. I didn’t care about backups until 1998, mainly because reapplying my settings after reinstalling the system was a tedious task.

I decided to begin from scratch and keep my configuration files organized after earning my engineering degree in 2024. Then I discovered I had several gigabytes of dotfiles. After spending weeks gathering and cleaning them up, I started this repository to reorganize everything.

To simplify things, I chose to remove configurations for software I no longer use and set up clean Linux installations on my personal computers to apply the snippets I found interesting and useful.

## What I use

  - **terminator** as my terminal.
  - **nerdfonts** as my font provider. [Here is the link.](https://www.nerdfonts.com/).
  - **zsh** as my command interpreter.
  - **oh my zsh** as an improvement on zsh.
  - **vim** as my terminal text editor.
  - **vimdiff** as my terminal diff viewer.
  - **vscodium** as my GUI text editor and diff viewer.
  - **git** as my version control system.
  - **editorconfig** as a simple text formatting tool.
  - **screen** as my default window multiplexer.
  - **tmux** as a fancy alternative for a window multiplexer.
  - **mc** as my terminal file manager.

## Local setup (personal)

I keep these files in subdirectories and link them into `$HOME` when setting up a machine.

Bear in mind that my whole enviroment makes use of the Dracula color theme.

```bash
mkdir -p "$HOME/.config/terminator"
ln -sf "$PWD/terminator/config" "$HOME/.config/terminator/config"
ln -sf "$PWD/zsh/zshenv" "$HOME/.zshenv"
ln -sf "$PWD/zsh/zprofile" "$HOME/.zprofile"
ln -sf "$PWD/zsh/zshrc" "$HOME/.zshrc"
ln -sf "$PWD/zsh/zshoptions" "$HOME/.zshoptions"
ln -sf "$PWD/zsh/zshaliases" "$HOME/.zshaliases"
ln -sf "$PWD/zsh/zshfunctions" "$HOME/.zshfunctions"
ln -sf "$PWD/git/gitconfig" "$HOME/.gitconfig"
ln -sf "$PWD/git/gitignore" "$HOME/.gitignore"
ln -sf "$PWD/git/gitattributes" "$HOME/.gitattributes"
ln -sf "$PWD/vim/vimrc" "$HOME/.vimrc"
ln -sf "$PWD/input/dircolors" "$HOME/.dircolors"
ln -sf "$PWD/input/inputrc" "$HOME/.inputrc"
```

### Desktop assets (`local/` → `~/.local/share`)

The `local/` directory holds GTK themes, icon themes, cursor themes, and fonts I use. They are not linked as a single tree; each pack is symlinked into the XDG data paths so desktops (GNOME, Cinnamon, Xfce, etc.) and fontconfig can find them.

- **`local/theme/`** → `~/.local/share/themes/` (one symlink per theme directory)
- **`local/icons/`** → `~/.local/share/icons/` (one symlink per icon theme)
- **`local/cursors/`** → `~/.local/share/icons/` (cursor themes use the same icon-theme layout; symlink each cursor pack by name)
- **`local/fonts/`** → `~/.local/share/fonts/` (one symlink per font file or directory)

Run from the repository root (same as above, with `cd` into the dotfiles directory first):

```bash
mkdir -p "$HOME/.local/share/themes" "$HOME/.local/share/icons" "$HOME/.local/share/fonts"

for d in "$PWD/local/theme"/*; do
  [ -d "$d" ] || continue
  ln -sfn "$d" "$HOME/.local/share/themes/$(basename "$d")"
done

for d in "$PWD/local/icons"/*; do
  [ -d "$d" ] || continue
  ln -sfn "$d" "$HOME/.local/share/icons/$(basename "$d")"
done

for d in "$PWD/local/cursors"/*; do
  [ -d "$d" ] || continue
  ln -sfn "$d" "$HOME/.local/share/icons/$(basename "$d")"
done

for d in "$PWD/local/fonts"/*; do
  [ -e "$d" ] || continue
  ln -sfn "$d" "$HOME/.local/share/fonts/$(basename "$d")"
done
```

After linking fonts, refresh the font cache: `fc-cache -f "$HOME/.local/share/fonts"`.

### Third-party assets and attribution

The files under `local/theme/`, `local/icons/`, `local/cursors/`, and `local/fonts/` are **not my original work**. I included copies in this repository **only** so I can install the same desktop look on my other machines without hunting packages each time. If you reuse or redistribute this repository (or those paths), you must still **comply with each upstream license** (retain notices, license texts where required, etc.).

| Asset | Upstream | License (see upstream for full text) |
| --- | --- | --- |
| **Orchis** GTK theme (including Dracula-coloured / compact variants under `local/theme/`) | [vinceliuice/Orchis-theme](https://github.com/vinceliuice/Orchis-theme) | GPL-3.0 |
| **Nerd Fonts** (`local/fonts/`) | [ryanoasis/nerd-fonts](https://github.com/ryanoasis/nerd-fonts) | SIL Open Font License 1.1 (per font; see upstream) |
| **Reversal** icon themes (`local/icons/`) | [yeyushengfan258/Reversal-icon-theme](https://github.com/yeyushengfan258/Reversal-icon-theme) | GPL-3.0 |
| **Bibata Modern Ice** cursors (`local/cursors/Bibata-Modern-Ice`) | [ful1e5/Bibata_Cursor](https://github.com/ful1e5/Bibata_Cursor) | GPL-3.0 |

## Readline vi quick usage

I use `~/.inputrc` with vi-style editing so readline-enabled programs behave more like Vim while keeping a few familiar Ctrl shortcuts in insert mode.

- Press `Esc` to switch from insert mode to command mode.
- In command mode, use `h`/`l` for left/right, `b`/`w` for word movement, and `0`/`$` for line start/end.
- History search is prefix-based with `Up`/`Down`, and also available with `Ctrl-p`/`Ctrl-n`.
- In insert mode, `Ctrl-a` and `Ctrl-e` still jump to the start/end of the line.

To quickly verify it after setup, start `bash` or `python3`, type a command, press `Esc`, and test the movement keys above.

## Ruby and PostgreSQL defaults

- I initialize Ruby with `rbenv` in interactive shells (`zshrc`).
- I initialize Node with `nvm` in interactive shells (`zshrc`).
- I set PostgreSQL defaults only when they are not already defined:
  - `PGHOST=localhost`
  - `PGPORT=5432`
  - `PGUSER=developer`
  - `PGPASSWORD=developer`
  - `PGDATABASE=development`

Project-specific values can still override these defaults, so this stays safe for local development.

## PostgreSQL helpers and optional tooling

I also added a few shell helpers:
- `pgstart`: start PostgreSQL service (`systemctl` or `pg_ctlcluster`).
- `pgstop`: stop PostgreSQL service (`systemctl` or `pg_ctlcluster`).
- `pglog`: follow PostgreSQL logs (`journalctl` or log file fallback).
- `psqlx`: open `psql` using current `PG*` env vars or local defaults.

For optional tooling, aliases/hooks are enabled only when the command exists:
- PostgreSQL: `pgcli` (`pg` alias), `pg_format` (`pgfmt` alias)
- Shell/productivity: `fzf` (`fzfp`), `fd` (`fdh`), `bat`/`batcat` (`bcat`), `eza` (`ezal`), `zoxide`, `direnv`
- Quality: `shellcheck` (`lintsh` function), `shfmt` (`fmtsh` function)

### Zoxide quick usage

- `z foo`: jump to the best directory match for `foo`
- `z foo bar`: jump using multiple search terms
- `zi foo`: interactive selection (with `fzf`)
- `z -`: jump back (similar to `cd -`)
- `zoxide query foo`: print the destination without changing directory

If I am setting up a Debian/Ubuntu machine, this is the install command I use:

```bash
sudo apt update
sudo apt install -y fonts-anonymous-pro postgresql-client pgcli pgformatter fzf fd-find bat eza zoxide direnv shellcheck shfmt
```

## Word of caution:

This repository is public as a way not to lose access to my own configuration files and user preferences, not for collaborative purposes, as I do not intend to maintain a history or ensure the consistency of this repository over time.

  - Read the files before using.
  - Extract snippets to adapt to your own dotfiles.
  - Do not use this repository on your own computers.
  - Do not fork this repository unless you know how to use it.

## Issues / Pull Requests

If you use this repository or part of it and find that something does not work correctly, you can open an issue in this GitHub repository. It is not necessary to open a pull request.
