# Uso del plugin ViM-TeX

Fuente https://github.com/lervag/vimtex

**Instalación**

```
   Plug 'lervag/vimtex'
```
## Requerimientos

**vimtex** requires the *clientserver* for the callback functionality to work.

En nuestro `.bashrc` o similar:

```
   alias vim='vim --servername VIM'
```

Si no funciona consultar  http://vim.wikia.com/wiki/Enable_servername_capability_in_vim/xterm

### Asegurar que detecta el `filetype`

Añadimos en el `.vimrc`

```
   let g:tex_flavor = 'latex'
```


## Inicio rápido

- Iniciar compilación con `\ll`
- Abrir *pdf* generado con `\lv`
- Ver errores con `\le`
- Limpiar archivos auxiliarer con `\lc`, con `\lC` eliminamos tambien el *pdf*
- Hacer un *reload* con `\lx`

## Uso

Activar al inicio con `let g:vimtex_enabled=1`

Activar/desactivar mapeos en modo insercción com `let g:vimtex_imaps_enabled=0/1`

Activar/desactivar mapeados para movimientos y el resaltado de los pares de delimitadores con `g:vimtex_motion_enabled=0`

Compilar al inicio, limpiar y cerrar paneles al salir:

```
   " Compile on initialization, cleanup on quit
  augroup vimtex_event_1
    au!
    au User VimtexEventQuit     call vimtex#compiler#clean(0)
    au User VimtexEventInitPost call vimtex#compiler#compile()
  augroup END

  " Close viewers on quit
  function! CloseViewers()
    if executable('xdotool') && exists('b:vimtex')
        \ && exists('b:vimtex.viewer') && b:vimtex.viewer.xwin_id > 0
      call system('xdotool windowclose '. b:vimtex.viewer.xwin_id)
    endif
  endfunction

  augroup vimtex_event_2
    au!
    au User VimtexEventQuit call CloseViewers()
  augroup END
```

### Completar

`let g:vimtex_complete_enabled=1` entonces es accesible con |i_CTRL-X_CTRL-O|.  

Integración con NeoComplete

```
   if !exists('g:neocomplete#sources#omni#input_patterns')
    let g:neocomplete#sources#omni#input_patterns = {}
  endif
  let g:neocomplete#sources#omni#input_patterns.tex =
        \ g:vimtex#re#neocomplete
```

### Documentación

Se proporciona el comando `VimtexDocPackage` (mapeado a `K`) que consultará en http://texdoc.net/ la documentación existente para un *package* o *documentclass*


