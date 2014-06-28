**eval-in-repl.el**
--------------------

This package does what ESS does for R for various REPLs, including ielm.

Emacs Speaks Statistics (ESS) package has a nice function called ess-eval-region-or-line-and-step, which is assigned to C-RET. This function sends a line or a selected region to the corresponding shell (R, Julia, Stata, etc) visibly. It also start up a shell if there is none.

This package implements similar work flow for various read-eval-print-loops (REPLs) shown below.

**Usage**
--------------------

After appropriate configuration (see below), you can use C-RET in a source file to start up an appropriate REPL and evaluate a line, selected region or the current expression depending on the context.


**Installation**
--------------------

The following files are included in the package. There are respective dependencies.

- eval-in-repl.el
 - Skeleton package required for all specialized packages below.

- eval-in-repl-ielm.el
 - Support for Inferior Emacs Lisp Mode (IELM; part of default emacs installation)

- eval-in-repl-cider.el
 - Support for Clojure via cider.el (depends on cider.el)

- eval-in-repl-slime.el
 - Support for other lisps via slime.el (depends on slime.el)

- eval-in-repl-scheme.el
 - Support for Scheme via scheme.el (depends on scheme.el; part of default emacs installation)

- eval-in-repl-python.el
 - Support for Python via python.el (depends on python.el; part of default emacs installation)

- eval-in-repl-shell.el (depends on essh.el)
 - Support for shell via essh.el


It is planned to be available on the MELPA repository. Once it becomes available you can do the following, then choose and install eval-in-repl.

To configure the MELPA, see this: http://melpa.milkbox.net/#/getting-started

```
M-x list-packages
```

**Configuration**
--------------------

The full configuration is the following. ```eval-in-repl``` is always necessary. Require other files as needed and configure the respective mode-specific key bindings.

```lisp
;; require the skeleton package
(require 'eval-in-repl)

;; cider
(require 'eval-in-repl-cider)
(define-key clojure-mode-map (kbd "<C-return>") 'eir-eval-in-cider)

;; ielm
(require 'eval-in-repl-ielm)
;; For .el files
(define-key emacs-lisp-mode-map (kbd "<C-return>") 'eir-eval-in-ielm)
;; For *scratch*
(define-key lisp-interaction-mode-map (kbd "<C-return>") 'eir-eval-in-ielm)
;; For M-x info
(define-key Info-mode-map (kbd "<C-return>") 'eir-eval-in-ielm)

;; SLIME
(require 'eval-in-repl-slime)
(add-hook 'lisp-mode-hook
		  '(lambda ()
		     (local-set-key (kbd "<C-return>") 'eir-eval-in-slime)))

;; scheme-mode
(require 'eval-in-repl-scheme)
(add-hook 'scheme-mode-hook
		  '(lambda ()
		     (local-set-key (kbd "<C-return>") 'eir-eval-in-scheme)))

;; python
(require 'eval-in-repl-python)
(define-key python-mode-map (kbd "<C-return>") 'eir-eval-in-python)

;; shell
(require 'eval-in-repl-shell)
(add-hook 'sh-mode-hook
          '(lambda()
		     (local-set-key (kbd "C-<return>") 'eir-eval-in-shell)))
```

**Special thanks:**
--------------------

This package is inspired by the wonderful Emacs Speaks Statistics (ESS) package.

<!-- mikeypostman and purcell for auditing the code for MELPA approval. -->