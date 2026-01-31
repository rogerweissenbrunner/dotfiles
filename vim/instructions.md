# Using VIM

## Vim Setup & Usage Guide

This guide explains how to install and use Vim with my current configuration.

### Installation

On Elementary OS, use:

```bash
sudo apt update
sudo apt -y install vim
```

To check if it works, use the following command:

```bash
which vim
vim --version
```

Take note of the version.

Copy the vimrc file to $HOME/.vimrc, and enable plugins.

Also, create the following directories:

```bash
mkdir -p $HOME/.vim/backup
mkdir -p $HOME/.vim/swap
mkdir -p $HOME/.vim/undodir
mkdir -p $HOME/.vim/snippets
```

### Plugins

This configuration uses vim's native `pack` system and includes the following plugins:

* Dracula Theme
* Fugitive
* NERDCommenter
* NERDTree
* EditorConfig
* Surround
* vim-snippets
* UltiSnips
* Emmet
* Highlighted Yank

#### On Vim 8.0

Create the following directories:

```bash
mkdir -p $HOME/.vim/pack/themes/opt
mkdir -p $HOME/.vim/pack/plugins/opt
```

Install plugins:

```bash
git clone https://github.com/dracula/vim.git $HOME/.vim/pack/themes/opt/dracula
git clone https://github.com/preservim/nerdtree.git $HOME/.vim/pack/plugins/opt/nerdtree
git clone https://github.com/preservim/nerdcommenter.git $HOME/.vim/pack/plugins/opt/nerdcommenter
git clone https://github.com/tpope/vim-fugitive.git $HOME/.vim/pack/plugins/opt/fugitive
git clone https://github.com/editorconfig/editorconfig-vim.git $HOME/.vim/pack/plugins/opt/editorconfig
git clone https://tpope.io/vim/surround.git $HOME/.vim/pack/plugins/opt/surround
git clone https://github.com/honza/vim-snippets.git $HOME/.vim/pack/plugins/opt/vim-snippets
git clone https://github.com/SirVer/ultisnips.git $HOME/.vim/pack/plugins/opt/ultisnips
git clone https://github.com/ycm-core/YouCompleteMe.git $HOME/.vim/pack/plugins/opt/youcompleteme
git clone https://github.com/mattn/emmet-vim.git $HOME/.vim/pack/plugins/opt/emmet-vim
git clone https://github.com/machakann/vim-highlightedyank.git $HOME/.vim/pack/plugins/opt/highlightedyank
git clone https://github.com/junegunn/vim-easy-align.git $HOME/.vim/pack/plugins/opt/easyalign
git clone https://github.com/airblade/vim-gitgutter.git $HOME/.vim/pack/plugins/opt/gitgutter
git clone https://github.com/vim-scripts/undotree.vim.git $HOME/.vim/pack/plugins/opt/undotree
git clone https://github.com/vim-airline/vim-airline.git $HOME/.vim/pack/plugins/opt/airline
```

#### On Vim 8.2+

Create the following directories:

```bash
mkdir -p $HOME/.vim/pack/themes/start
mkdir -p $HOME/.vim/pack/plugins/start  
```

Install plugins:
```bash
git clone https://github.com/dracula/vim.git $HOME/.vim/pack/themes/start/dracula
git clone https://github.com/preservim/nerdtree.git $HOME/.vim/pack/plugins/start/nerdtree
git clone https://github.com/preservim/nerdcommenter.git $HOME/.vim/pack/plugins/start/nerdcommenter
git clone https://github.com/tpope/vim-fugitive.git $HOME/.vim/pack/plugins/start/fugitive
git clone https://github.com/editorconfig/editorconfig-vim.git $HOME/.vim/pack/plugins/start/editorconfig
git clone https://tpope.io/vim/surround.git $HOME/.vim/pack/plugins/start/surround
git clone https://github.com/honza/vim-snippets.git $HOME/.vim/pack/plugins/start/vim-snippets
git clone https://github.com/SirVer/ultisnips.git $HOME/.vim/pack/plugins/start/ultisnips
git clone https://github.com/ycm-core/YouCompleteMe.git $HOME/.vim/pack/plugins/start/youcompleteme
git clone https://github.com/mattn/emmet-vim.git $HOME/.vim/pack/plugins/start/emmet-vim
git clone https://github.com/machakann/vim-highlightedyank.git $HOME/.vim/pack/plugins/start/highlightedyank
git clone https://github.com/junegunn/vim-easy-align.git $HOME/.vim/pack/plugins/start/easyalign
git clone https://github.com/airblade/vim-gitgutter.git $HOME/.vim/pack/plugins/start/gitgutter
git clone https://github.com/vim-scripts/undotree.vim.git $HOME/.vim/pack/plugins/start/undotree
git clone https://github.com/vim-airline/vim-airline.git $HOME/.vim/pack/plugins/start/airline
```

### Vim Basics

#### Learning to quit vim

In normal vim, you can quit by pressing **ESC** and typing `:q!`.

| Action      | Shortcut |
| ----------- | -------- |
| Save        | `:w!`    |
| Quit        | `:q`     |
| Save & Quit | `:wq!`   |
| Force Quit  | `:q!`    |

`,` is your **leader key**. You need to press **ESC** before entering shortcuts. The **ESC** key allows you to enter a mode where you can type commands without writing.

#### Vim Modes

When you begin working with vim, you begin in "normal mode", where you can navigate files and execute vim commands.

| Mode    | What it does        |
| ------- | ------------------- |
| NORMAL  | Navigate & commands |
| INSERT  | Type text           |
| VISUAL  | Select text         |
| COMMAND | Run commands        |

To enter INSERT mode and be able to type, you should press letter "i".
To get back to NORMAL mode, you should press the "ESC" key.

#### Moving

Once you get into NORMAL mode, you can navigate your document with the following keys:

| Action | Keystrokes |
| ------ | ---------- |
| left   | `h`        |
| right  | `l`        |
| down   | `j`        |
| up     | `k`        |

You can also use the arrow keys, but using these enable you to understand the following custom mappings to move faster:

| Action              | Keystrokes |
| ------------------- | ---------- |
| move down 8 lines   | `,j`       |
| move up 8 lines     | `,k`       |
| go to start of line | `,h`       |
| go to end of line   | `,l`       |

To jump around you can also use these keys:

| Action         | Keystrokes |
| -------------- | ---------- |
| top of file    | `gg`       |
| bottom of file | `G`        |
| next word      | `w`        |
| previous word  | `b`        |
| start of line  | `0`        |
| end of line    | `$`        |

#### Editing Text

Deleting text can be done like this:

| Action              | Keystrokes |
| ------------------- | ---------- |
| delete character    | `x`        |
| delete 5 characters | `5x`       |
| delete line         | `dd`       |
| delete 5 lines      | `5dd`      |
| delete word         | `dw`       |
| delete 5 words      | `5dw`      |
| delete to the end   | `d$`       |

"Deleting something" removes it from the text, but the result goes to the clipboard, it can be pasted.

| Action       | Keystrokes |
| ------------ | ---------- |
| copy line    | `yy`       |
| copy 5 lines | `5yy`      |
| paste below  | `p`        |
| paste above  | `P`        |

Searching is also a combination of commands. You can search for "word" by writing `/word` in normal mode.

| Action                   | Keystrokes |
| ------------------------ | ---------- |
| next match to the bottom | `n`        |
| next match to the top    | `N`        |
| clear highlighting       | `,/`       |

### Splits and Windows

Each split creates a new window.

| Action           |  Keystrokes |
| ---------------- |  ---------- |
| vertical split   |  `,v`       |
| horizontal split |  `,s`       |

Moving between windows can be done with `,w` and the direction.

| Action     | Keystrokes |
| ---------- | ---------- |
| move left  | `,wh`      |
| move right | `,wl`      |
| move down  | `,wj`      |
| move up    | `,wk`      |

Resizing windows can be done with a couple strokes.

| Action          | Keystrokes |
| --------------- | ---------- |
| increase width  | `,>`       |
| decrease width  | `,<`       |
| increase height | `,+`       |
| decrease height | `,-`       |

Besides windows, we can work with tabs.

| Action        | Keystrokes |
| ------------- | ---------- |
| new tab       | `,tn`      |
| close tab     | `,tc`      |
| only this tab | `,to`      |
| next tab      | `,tt`      |
| previous tab  | `,tT`      |

### NERDTree (File Explorer)

The file explorer will split the current window.

| Action         | Keystrokes |
| -------------- | ---------- |
| open file tree | `,nt`      |

Inside NERDTree you have the following actions:

| Action          | Keystrokes |
| --------------- | ---------- |
| open file       | `o`        |
| open in new tab | `t`        |
| split           | `s`        |
| vertical split  | `v`        |
| file menu       | `m`        |
| help            | `?`        |

### NERDCommenter

These actions work in NORMAL mode.

| Action          | Keystrokes |
| --------------- | ---------- |
| comment code    | `,cc`      |
| uncomment       | `,cu`      |
| toggle          | `,cc`      |

### YouCompleteMe

Installing YouCompleteMe isn't as straightforward as other plugins.

```bash
cd $HOME/.vim/pack/plugins/opt/youcompleteme
git submodule update --init --recursive
sudo apt -y install python3-dev cmake
python3 install.py --ts-completer
```

# FROM HERE ONWARDS I HAVEN'T CHECKED THIS!

# 12. Git Integration (vim-fugitive)

Inside a Git repo:

Open Git status:

```
:Git
```

Stage file:

```
-
```

Commit:

```
cc
```

View diff:

```
:Git diff
```

---

# 13. Useful Built-in Tricks

## Repeat Last Command

```
.
```

## Undo / Redo

```
u
Ctrl+r
```

## Visual Mode

Select text:

```
v
```

Line select:

```
V
```

Block select:

```
Ctrl+v
```

# ✍️ 3. Editing Improvements

### Show Invisible Characters

```vim
set list
set listchars=tab:▸\ ,trail:·
```

You’ll see trailing spaces.
