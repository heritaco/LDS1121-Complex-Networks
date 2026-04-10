# Proyecto LaTeX: ensayo sobre redes biológicas

## Archivos
- `main.tex`: documento principal.
- `biblio.bib`: base bibliográfica en formato BibTeX/BibLaTeX.

## Compilación
En este equipo, `xelatex` falla al generar el PDF final con la fuente `EB Garamond`.
La forma más estable de compilar es con `lualatex` usando `latexmk`, que ejecuta `biber`
automáticamente:

```bash
latexmk -lualatex -interaction=nonstopmode -synctex=1 main.tex
```

Si prefieres compilar manualmente:

```bash
lualatex main.tex
biber main
lualatex main.tex
lualatex main.tex
```

## Observaciones
- El texto está redactado en español académico natural.
- Incluye notas a pie de página y referencias bibliográficas.
- La bibliografía se formatea con estilo APA mediante `biblatex`.

# Instruccion de la tarea

Realiza un ensayo sobre redes biológicas

- ¿Cuáles son las redes dentro de la clase? 
- ¿Cómo se caracterizan?
- ¿Qué propiedades tienen?
- ¿Cómo se modelan?
- ¿Qué podemos aprender de ellas?
- ¿Son importantes? ¿Por qué?
- ¿Qué tipo de problemas se resuelven?


Los elementos del ensayo son:  Título, Introducción, Argumentación, Conclusión, Notas a pie de página y Referencias.





