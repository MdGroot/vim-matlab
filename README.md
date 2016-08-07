vim-matlab
===========

An alternative to Matlab's default editor for Vim users.

### Usage

`vim-matlab` works by remotely controlling a CLI Matlab instance (launched by `vim-matlab-server.py`).

Run

```
./scripts/vim-matlab-server.py
```

This will start a Matlab REPL and redirect commands received from Vim to Matlab. When Matlab crashes (e.g. segfault during MEX development), it will launch another process.

Then open Vim in another terminal and start editing .m files.

- `:MatlabCliCancel` (\<leader\>c) tells the server to send SIGINT to Matlab, canceling current operation.

- `:MatlabCliRunSelection` executes the highlighted Matlab code.

- `:MatlabCliRunCell` executes code in the current cell — i.e. `%%` blocks. Similar to Ctrl-Enter in the Matlab editor.

- `:MatlabCliOpenInEditor` (,e) opens current buffer in a Matlab editor window. e.g. to access the debugger.

- `:MatlabCliHelp` (,h) prints help message for the word under the cursor.

- `:MatlabNormalModeCreateCell` (C-l) inserts a cell marker above the current line.

- `:MatlabVisualModeCreateCell` (C-l) inserts cell markers above and below the visual selection.

- `:MatlabInsertModeCreateCell` (C-l) inserts a cell marker at the beginning of the current line.

See [this file](rplugin/python/vim_matlab/__init__.py) for a list of available commands, and [vim-matlab.vim](ftplugin/matlab/vim-matlab.vim) for default key bindings.

![Screenshot](/docs/images/screenshot.png)

### Installation

Install the python3 client for Neovim.

```
pip3 install neovim
```

Add to `.vimrc` (or `~/.config/nvim/init.vim`). e.g. using [vim-plug](https://github.com/junegunn/vim-plug),

```
Plug 'daeyun/vim-matlab'
```

Install and run `:UpdateRemotePlugins`

Optionally install [SirVer/ultisnips](https://github.com/honza/vim-snippets) to use the snippets.


### Configuration

Use this option to prevent the plugin from automatically generating key mappings (default = 1).

```
let g:matlab_auto_mappings = 0
```


### Development

Set up a symlink so that the plugin directory points to your repository.

```
git clone git@github.com:daeyun/vim-matlab.git
rm -r ~/.vim/plugged/vim-matlab
ln -nsf $(pwd)/vim-matlab ~/.vim/plugged/
```

After changing the code, run `scripts/reload-vim.sh` (optionally pass in a file to open) to reload.

For testing, install [pytest](https://github.com/pytest-dev/pytest/) and run `scripts/run-tests.sh`.


### Recommended Plugins

- [MatlabFilesEdition](http://www.vim.org/scripts/script.php?script_id=2407)
- [matchit.zip](http://www.vim.org/scripts/script.php?script_id=39)
