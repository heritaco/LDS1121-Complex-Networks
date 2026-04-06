# Proyecto LaTeX: ensayo sobre redes biológicas

## Archivos
- `main.tex`: documento principal.
- `biblio.bib`: base bibliográfica en formato BibTeX/BibLaTeX.

## Compilación
Compila con `biber`:

```bash
pdflatex main.tex
biber main
pdflatex main.tex
pdflatex main.tex
```

## Observaciones
- El texto está redactado en español académico natural.
- Incluye notas a pie de página y referencias bibliográficas.
- La bibliografía se formatea con estilo APA mediante `biblatex`.
