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




