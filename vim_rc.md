n('~/.vim/plugged')
Plug 'bling/vim-airline'
Plug 'xolox/vim-notes'
Plug 'xolox/vim-misc'
Plug 'tpope/vim-surround'
Plug 'godlygeek/tabular'
Plug 'tpope/vim-fugitive'
call plug#end()

" Mi leaderKey pasa a ser Space
let mapleader = "\<Space>"

filetype plugin on
filetype indent on

" Nuevas ventanas a la derecha
set splitright

" Forzar que un .md se vea como tipo markdown
autocmd BufNewFile,BufReadPost *.md set filetype=markdown

set autoread

" Interface
"set wildmenu
"set ruler
set number
"set cmdheight=1
"set ignorecase
"set smartcase
"set magic
"set showmatch
"set mousehide

" Colores y Fuentes
syntax enable
colorscheme dracula
"call togglebg#map("<F5>")
"set background=dark
set encoding=utf8
"set ffs=unix,dos,mac
autocmd BufNewFile,BufReadPost *.md set filetype=markdown
set guifont=Sauce_Code_Powerline:h10
set guioptions=aAce
" set columns=100

" Ficheros, backup
set nobackup
set nowb
set noswapfile

" Texto, tab
set expandtab
set smarttab
set shiftwidth=2
set tabstop=4
set textwidth=79
set lbr
set ai
set si
set wrap
" no continua comentario en lía siguiente
au FileType * set fo-=cro
" desactivar indentaciónnoremap <F2> :set invpaste paste?<CR>
set pastetoggle=<F2>
set showmode

" Status line
"set laststatus=2

" Movimiento entre lías de forma NATURAL
nnoremap j gj
nnoremap k gk

" Salir de INSERT MODE con jj
inoremap <special> jj <ESC>

" Guardar con ww en INSERT MODE
inoremap ww <ESC>:w<CR>

" Guardar con w
nnoremap <Leader>w :w<CR>

" VSplit y HSplit
nnoremap <Leader>v :vsplit<CR>
nnoremap <Leader>h :split<CR>

" Moverse entre ventanas
nnoremap <Leader><Tab> <C-W><C-W>

" Pasar a la ventana de la derecha, izquierda, arriba, abajo
" esta feo usar los cursores ;)
nnoremap <Leader><Right> <C-W><C-L>
nnoremap <Leader><Left> <C-W><C-H>
nnoremap <Leader><Up> <C-W><C-K>
nnoremap <Leader><Down> <C-W><C-J>
" Para el trabajo: entrecomillar
nnoremap <Leader>i :%s/^/'<CR>
nnoremap <Leader>f :%s/$/',<CR>

let g:nord_comment_brightness = 18

set nospell
set cursorline
set relativenumber
" Clipboard del sistema
map gy "*y
"" Copia todo el fichero al clipboard del sistema
nmap gY gg"*yG

augroup autosourcing
    autocmd!
    autocmd BufWritePost .vimrc source %
augroup END

