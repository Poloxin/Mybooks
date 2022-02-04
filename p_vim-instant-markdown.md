# Plugin vim-instant-markdown

When you open a markdown file in Vim, a browser window will open which shows the compiled markdown in real-time, and closes once you close the file in Vim.

## Installation

You need install the Python mini-server

```
pip install --user smdv
```

Add the following to your `.vimrc` to vim-plug section:

```vim
Plug 'instant-markdown/vim-instant-markdown', {'for': 'markdown', 'do': 'yarn install'}
```

**Addictions:**

- `xdg-utils`

- `curl`

- `nodejs`

## Configuration

Minimal default configuration:

```vim
filetype plugin on
"Uncomment to override defaults:
"let g:instant_markdown_slow = 1
"let g:instant_markdown_autostart = 0
"let g:instant_markdown_open_to_the_world = 1
"let g:instant_markdown_allow_unsafe_content = 1
"let g:instant_markdown_allow_external_content = 0
"let g:instant_markdown_mathjax = 1
"let g:instant_markdown_mermaid = 1
"let g:instant_markdown_logfile = '/tmp/instant_markdown.log'
"let g:instant_markdown_autoscroll = 0
"let g:instant_markdown_port = 8888
"let g:instant_markdown_python = 1
```
