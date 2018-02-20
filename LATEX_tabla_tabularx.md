# Latex tablas con el paquete tabularx

En el preámbulo

```tex
  \usepackage{tabularx}
  % Para centrar contenido en las columnas
  \newcolumntype{Y}{>{\centering\arraybackslash}X}
  ...
  document
  ...
  \begin{tabularx}{\textwidth}{ X|Y|X }
  Uno & $\longrightarrow$ & dos \\
  \end{tabularx}
