<p align="center">
<a href="https://github.com/CardozoCasariegoLuciano/pruebaMD">English</a> |
  <span>Español</span>  
</p>


<img src="https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.png" height="75" alt="vim-plug">[![travis-ci](https://travis-ci.org/junegunn/vim-plug.svg?branch=master)](https://travis-ci.org/junegunn/vim-plug)
===

Un administrador de plugins minimalista para Vim.

<img src="https://raw.githubusercontent.com/junegunn/i/master/vim-plug/installer.gif" height="450">

### Pros.

- Fácil de iniciar: Un único archivo. Sin código repetido.
- Fácil de usar: Conciso, sintaxis intuitiva
- Instalación/actualización en paralelo [Super-rapida][40/4]
   (con cualquiera de: `+job`, `+python`, `+python3`, `+ruby`, o [Neovim][nv])
- Crea clones simples para minimizar uso de disco y tiempo de descarga
- Carga a demanda con [faster startup time][startup-time]
- Puedes revisar y revertir actualizaciones
- Soporte para branch/tag/commit
- Ganchos post-actualización
- Soporte para complementos externos


[40/4]: https://raw.githubusercontent.com/junegunn/i/master/vim-plug/40-in-4.gif
[nv]: http://neovim.org/
[startup-time]: https://github.com/junegunn/vim-startuptime-benchmark#result

### Instalación

[Descarga plug.vim](https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim)
y peguelo en el directorio "autoload".

#### Vim

###### Unix

```sh
curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```

Puede automatizar el proceso poniendo el comando en su archivo de configuración
de vim, tal como sugerimos [aquí][auto].


[auto]: https://github.com/junegunn/vim-plug/wiki/tips#automatic-installation

###### Windows (PowerShell)

```powershell
iwr -useb https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim |`
    ni $HOME/vimfiles/autoload/plug.vim -Force
```

#### Neovim

###### Unix, Linux

```sh
sh -c 'curl -fLo "${XDG_DATA_HOME:-$HOME/.local/share}"/nvim/site/autoload/plug.vim --create-dirs \
       https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim'
```

###### Linux (Flatpak)

```sh
curl -fLo ~/.var/app/io.neovim.nvim/data/nvim/site/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```

###### Windows (PowerShell)

```powershell
iwr -useb https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim |`
    ni "$(@($env:XDG_DATA_HOME, $env:LOCALAPPDATA)[$null -eq $env:XDG_DATA_HOME])/nvim-data/site/autoload/plug.vim" -Force
```

### Obteniendo ayuda
 
- Consulte la página [tutorial] para aprender las bases de vim-plug
- Consulte las paginas [tips] y [FAQ] por problemas comunes y preguntas
- Consulte la página [requisitos] para obtener información sobre depuración y configuraciones probadas
- Cree un [issue](https://github.com/junegunn/vim-plug/issues/new)
 
[tutorial]: https://github.com/junegunn/vim-plug/wiki/tutorial
[tips]: https://github.com/junegunn/vim-plug/wiki/tips
[FAQ]: https://github.com/junegunn/vim-plug/wiki/faq
[requirements]: https://github.com/junegunn/vim-plug/wiki/requirements

### Uso

Añada una sección para vim-plug en su `~/.vimrc` (o `stdpath('config') . '/init.vim'` para Neovim)
 
1. Comience la sección con `call plug#begin()`
1. Liste los plugins con el comando `Plug`
1. Finalice la sección con `call plug#end()` para actualizar `&runtimepath` e inicializar el sistema de plugin
   - Automáticamente ejecuta `filetype plugin indent on` y `syntax enable`.
     Puede revertir estas configuraciones luego del llamado. ej: `filetype indent off`, `syntax off`, etc.

#### Ejemplo

```vim
" Specify a directory for plugins
" - For Neovim: stdpath('data') . '/plugged'
" - Avoid using standard Vim directory names like 'plugin'
call plug#begin('~/.vim/plugged')

" Make sure you use single quotes

" Shorthand notation; fetches https://github.com/junegunn/vim-easy-align
Plug 'junegunn/vim-easy-align'

" Any valid git URL is allowed
Plug 'https://github.com/junegunn/vim-github-dashboard.git'

" Multiple Plug commands can be written in a single line using | separators
Plug 'SirVer/ultisnips' | Plug 'honza/vim-snippets'

" On-demand loading
Plug 'scrooloose/nerdtree', { 'on':  'NERDTreeToggle' }
Plug 'tpope/vim-fireplace', { 'for': 'clojure' }

" Using a non-default branch
Plug 'rdnetto/YCM-Generator', { 'branch': 'stable' }

" Using a tagged release; wildcard allowed (requires git 1.9.2 or above)
Plug 'fatih/vim-go', { 'tag': '*' }

" Plugin options
Plug 'nsf/gocode', { 'tag': 'v.20150303', 'rtp': 'vim' }

" Plugin outside ~/.vim/plugged with post-update hook
Plug 'junegunn/fzf', { 'dir': '~/.fzf', 'do': './install --all' }

" Unmanaged plugin (manually installed and updated)
Plug '~/my-prototype-plugin'

" Initialize plugin system
call plug#end()
```

Recargue el .vimrc y ejecute `:PlugInstall` para instalar los plugins

### Comandos

| Comando                             | Descripcion                                                        |
| ----------------------------------- | ------------------------------------------------------------------ |
| `PlugInstall [name ...] [#threads]` | Instalar plugins                                                   |
| `PlugUpdate [name ...] [#threads]`  | Instalar o actualizar plugins                                      |
| `PlugClean[!]`                      | Remover plugins sin listar                                         |
| `PlugUpgrade`                       | Actualizar vim-plug                                                |
| `PlugStatus`                        | Verificar el estado de los plugins                                 |
| `PlugDiff`                          | Examinar cambios entre la ultima actualizacion y los cambios pendientes |
| `PlugSnapshot[!] [output path]`     | Generar un script para restaurar el snapshot actual de plugins     |

### Opciones `Plug` 

| Opcion                  | Descripcion                                      |
| ----------------------- | ------------------------------------------------ |
| `branch`/`tag`/`commit` | Branch/tag/commit del repositorio a usar         |
| `rtp`                   | Subdirectorio qie contenga Vim Plugin            |
| `dir`                   | Directorio personalizado para plugins            |
| `as`                    | Usar un nombre distinto para el plugin           |
| `do`                    | Post-update hook (string or funcref)             |
| `on`                    | On-demand loading: Commands or `<Plug>`-mappings |
| `for`                   | On-demand loading: File types                    |
| `frozen`                | Do not update unless explicitly specified        |

### Global options

| Flag                | Default                           | Description                                            |
| ------------------- | --------------------------------- | ------------------------------------------------------ |
| `g:plug_threads`    | 16                                | Default number of threads to use                       |
| `g:plug_timeout`    | 60                                | Time limit of each task in seconds (*Ruby & Python*)   |
| `g:plug_retries`    | 2                                 | Number of retries in case of timeout (*Ruby & Python*) |
| `g:plug_shallow`    | 1                                 | Use shallow clone                                      |
| `g:plug_window`     | `vertical topleft new`            | Command to open plug window                            |
| `g:plug_pwindow`    | `above 12new`                     | Command to open preview window in `PlugDiff`           |
| `g:plug_url_format` | `https://git::@github.com/%s.git` | `printf` format to build repo URL (Only applies to the subsequent `Plug` commands) |


### Keybindings

- `D` - `PlugDiff`
- `S` - `PlugStatus`
- `R` - Retry failed update or installation tasks
- `U` - Update plugins in the selected range
- `q` - Close the window
- `:PlugStatus`
    - `L` - Load plugin
- `:PlugDiff`
    - `X` - Revert the update

### Example: A small [sensible](https://github.com/tpope/vim-sensible) Vim configuration

```vim
call plug#begin()
Plug 'tpope/vim-sensible'
call plug#end()
```

### On-demand loading of plugins

```vim
" NERD tree will be loaded on the first invocation of NERDTreeToggle command
Plug 'scrooloose/nerdtree', { 'on': 'NERDTreeToggle' }

" Multiple commands
Plug 'junegunn/vim-github-dashboard', { 'on': ['GHDashboard', 'GHActivity'] }

" Loaded when clojure file is opened
Plug 'tpope/vim-fireplace', { 'for': 'clojure' }

" Multiple file types
Plug 'kovisoft/paredit', { 'for': ['clojure', 'scheme'] }

" On-demand loading on both conditions
Plug 'junegunn/vader.vim',  { 'on': 'Vader', 'for': 'vader' }

" Code to execute when the plugin is lazily loaded on demand
Plug 'junegunn/goyo.vim', { 'for': 'markdown' }
autocmd! User goyo.vim echom 'Goyo is now loaded!'
```

The `for` option is generally not needed as most plugins for specific file types
usually don't have too much code in the `plugin` directory. You might want to
examine the output of `vim --startuptime` before applying the option.

### Post-update hooks

There are some plugins that require extra steps after installation or update.
In that case, use the `do` option to describe the task to be performed.

```vim
Plug 'Shougo/vimproc.vim', { 'do': 'make' }
Plug 'ycm-core/YouCompleteMe', { 'do': './install.py' }
```

If the value starts with `:`, it will be recognized as a Vim command.

```vim
Plug 'fatih/vim-go', { 'do': ':GoInstallBinaries' }
```

If you need more control, you can pass a reference to a Vim function that
takes a single argument.

```vim
function! BuildYCM(info)
  " info is a dictionary with 3 fields
  " - name:   name of the plugin
  " - status: 'installed', 'updated', or 'unchanged'
  " - force:  set on PlugInstall! or PlugUpdate!
  if a:info.status == 'installed' || a:info.force
    !./install.py
  endif
endfunction

Plug 'ycm-core/YouCompleteMe', { 'do': function('BuildYCM') }
```

Both forms of post-update hook are executed inside the directory of the plugin
and only run when the repository has changed, but you can force it to run
unconditionally with the bang-versions of the commands: `PlugInstall!` and
`PlugUpdate!`.

Make sure to escape BARs and double-quotes when you write the `do` option inline
as they are mistakenly recognized as command separator or the start of the
trailing comment.

```vim
Plug 'junegunn/fzf', { 'do': 'yes \| ./install' }
```

But you can avoid the escaping if you extract the inline specification using a
variable (or any Vimscript expression) as follows:

```vim
let g:fzf_install = 'yes | ./install'
Plug 'junegunn/fzf', { 'do': g:fzf_install }
```

### `PlugInstall!` and `PlugUpdate!`

The installer takes the following steps when installing/updating a plugin:

1. `git clone` or `git fetch` from its origin
2. Check out branch, tag, or commit and optionally `git merge` remote branch
3. If the plugin was updated (or installed for the first time)
    1. Update submodules
    2. Execute post-update hooks

The commands with the `!` suffix ensure that all steps are run unconditionally.

### Articles

- [Writing my own Vim plugin manager](http://junegunn.kr/2013/09/writing-my-own-vim-plugin-manager)
- [Vim plugins and startup time](http://junegunn.kr/2014/07/vim-plugins-and-startup-time)
- ~~[Thoughts on Vim plugin dependency](http://junegunn.kr/2013/09/thoughts-on-vim-plugin-dependency)~~
    - *Support for Plugfile has been removed since 0.5.0*

### Collaborators

- [Jan Edmund Lazo](https://github.com/janlazo) - Windows support
- [Jeremy Pallats](https://github.com/starcraftman) - Python installer

### License

MIT
