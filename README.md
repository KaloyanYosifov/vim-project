## Introduction
A Project is made of :
* One directory (the ``root of the project``)
* One title (by default the last part of the the ``root of the project``)
* One or more ``callbacks``

Everytime you open a file nested in the ``root of the project``
* the ``local current directory`` is changed to the ``root of the project``
* the ``guitablabel`` is set to the ``title`` of the project
* the ``callbacks`` of the project are executed

![img][0]

## Commands
There are four commands :
* ``Project``
It's used inside the ``.vimrc``. The first parameter is the ``path`` to the
project. The second parameter is optional and it is the ``title`` of the
project and the default value of it is the last part of the name of the
directory containing the project.  If the ``path`` to the project is a
relative path, it's combined with the ``starting path``.  The ``starting
path`` is defined when you initialize the plugin :

```vim
set rtp+=~/.vim/bundle/vim-project/
" custom starting path
call project#rc("~/Code")
" default starting path (the home directory)
call project#rc()
```

* ``ProjectPath``
It's used inside the ``cmdline mode``. The first parameter is the ``path``
without quotation. The second parameter is optional and it is the ``title`` of
the project without quotation.
If the ``path`` to the project is a relative path, it's combined with
``current working directory`` and **not** with the ``starting path``.
* ``File``
It's used inside the ``.vimrc``. The first parameter is the ``path`` to
the file. The second parameter is the ``title`` of the file. This command
doesn't change the ``local current directory``.
* ``Callback``
It's used inside the ``.vimrc``. The first parameter is the ``title`` of a
project already defined with ``Project`` or ``File``. The second parameter is
the name a function or an array of function names. This function or these
functions are callbacks and they are executed everytime a file nested in the
``root of the project`` is opened with **one parameter** that is the ``title``
of the project.
* ``Welcome`` It's the [``Startify``](https://github.com/mhinz/vim-startify) equivalent.
If you don't want ``Welcome`` to appear when you start vim:

```vim
" before call project#rc()
let g:project_enable_welcome = 0
" if you want the NERDTree integration.
let g:project_use_nerdtree = 1

set rtp+=~/.vim/bundle/vim-project/
call project#rc("~/Code")
```

![Welcome](https://pbs.twimg.com/media/BJH4RgDCcAEYv4E.png:large)

## Install
If you use [Vundle][1] you can install this plugin using Vim command `:BundleInstall amiorin/vim-project`.
Don't forget put a line `Bundle 'amiorin/vim-project'` in your `.vimrc`.

If you use [Pathogen][2], you just execute following:

```sh
cd ~/.vim/bundle
git https://github.com/amiorin/vim-project.git
```

If you don't use either plugin management system, copy the `plugin` directory to your `.vim` directory.

\*nix: $HOME/.vim
Windows: $HOME/vimfiles

## Configure
sample ``.vimrc``:

```vim
let g:project_use_nerdtree = 1
set rtp+=~/.vim/bundle/vim-project/
call project#rc("~/Code")

Project  'scratch'

Project  'dotfiles'
File     'dotfiles/vimrc'                       , 'vimrc'
File     'dotfiles/gvimrc'                      , 'gvimrc'
File     'dotfiles/zshrc'                       , 'zshrc'

Project  'gollum'
File     'gollum/Todo.md'                       , 'todo'
Callback 'gollum'                               , 'RemoveTextWidth'

function! RemoveTextWidth(...) abort
  setlocal textwidth=0
endfunction

Project  'octopress'
Project  'gsource'
Project  'markup'
Project  'glib'
Project  'reloadlive'
Project  'flashcards'
Project  'leitner'
Callback 'leitner'                              , ['AddSpecToPath', 'RemoveTextWidth']

function! AddSpecToPath(tile) abort
  setlocal path+=spec
endfunction

Project  '~/.vim/bundle/vim-fenced-code-blocks' , 'fenced'
Project  '~/.vim/bundle/vim-project'            , 'project'
Project  '~/.vim/bundle/vim-bookmarks'          , 'bookmarks'
Project  '~/.vim/bundle/ctrlp.vim'              , 'ctrlp'
Project  '~/.vim/bundle/ctrlp-z'                , 'ctrlp-z'
Project  '~/.vim/bundle/vim-eval'               , 'eval'
```

## Interactive
From the ``cmdline mode``.

``ProjectPath`` uses the ``cwd`` and the arguments are not quoted.
```vim
:ProjectPath .
:ProjectPath /etc myconfig
```

## Self-Promotion
Like this plugin?
* Star the repository on [GitHub](https://github.com/amiorin/vim-project)
* Follow me on
  * [Twitter](http://twitter.com/amiorin)
  * [GitHub](https://github.com/amiorin)
  * [Blog](http://albertomiorin.com)

[0]: https://pbs.twimg.com/media/BIcCUupCMAEG8Lg.png:large
[1]: https://github.com/gmarik/vundle.git
[2]: https://github.com/tpope/vim-pathogen
