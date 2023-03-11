# Elixir Major Mode using tree-sitter

[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)
[![MELPA](https://melpa.org/packages/elixir-ts-mode-badge.svg)](https://melpa.org/#/elixir-ts-mode)

For an implementation without tree-sitter support please have a
look at: https://github.com/elixir-editors/emacs-elixir

This package is compatible with and was tested against the tree-sitter grammar
for Elixir found at https://github.com/elixir-lang/tree-sitter-elixir.

## Installing

Emacs 29.1 or above with tree-sitter support is required. 

Tree-sitter starter guide: https://git.savannah.gnu.org/cgit/emacs.git/tree/admin/notes/tree-sitter/starter-guide?h=emacs-29

### Using MELPA and use-package

```elisp
(use-package elixir-ts-mode
    :ensure t)
```

### From source

- Clone this repository
- Add the following to your emacs config

It is also necessary to clone 
[heex-ts-mode](https://github.com/wkirschbaum/heex-ts-mode) and
load the heex-ts-mode.el file before loading elixir-ts-mode.el:

```elisp
(load "[cloned wkirschbaum/heex-ts-mode]/heex-ts-mode.el")
(load "[cloned wkirschbaum/elixir-ts-mode]/elixir-ts-mode.el")
```

### Using with Eglot

```elisp
(require 'eglot)

(dolist (mode '(elixir-ts-mode heex-ts-mode))
    (add-to-list 'eglot-server-programs `(,mode . ("[elixir language server path]"))))

(add-hook 'elixir-ts-mode-hook 'eglot-ensure)
(add-hook 'heex-ts-mode-hook 'eglot-ensure)
```

### Using with lsp-mode

Ensure to add elixir-ts-mode and heex-ts-mode hooks ( refer to https://emacs-lsp.github.io/lsp-mode/page/installation/ )

```
(elixir-ts-mode . lsp)
(heex-ts-mode   . lsp)
```

While [this change](https://github.com/emacs-lsp/lsp-mode/pull/3883)
has not been released, you can add the following so long:

```elisp
(require 'lsp-mode)

(setq lsp-language-id-configuration
      (append lsp-language-id-configuration
              '((elixir-ts-mode . "elixir")
                (heex-ts-mode . "elixir"))))
```

### Installing emacs-29 on Mac OS or Linux via Homebrew

```bash
brew install tree-sitter
brew install emacs-plus@29
```

## Development

To test you can run `make test` which will download a batch script
from https://github.com/casouri/tree-sitter-module and compile
tree-sitter-elixir as well as tree-sitter-heex. 

Requirements:

- tree-sitter
- make
- gcc
- git
- curl


Please make sure you run `M-x byte-compile-file` against the updated
file(s) with an emacs version --with-tree-sitter=no to ensure it still
works for non tree-sitter users. 
