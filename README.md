# LDS1121 Complex Networks

Material de trabajo para actividades y notebooks de redes complejas.

El repositorio incluye ejercicios de `NetworkX`, medidas de centralidad, modelos aleatorios, modularidad, agrupamiento espectral y prediccion de enlaces, junto con datos auxiliares para las practicas.

## Estructura

- `notebooks/`: cuadernos organizados por tema.
- `data/`: bases de datos y archivos de entrada para los ejercicios.
- `helpers/`: scripts de apoyo para conversion o preparacion de datos.

## Entorno recomendado

Este proyecto usa un entorno de `conda` llamado `redes`.

### Crear el entorno desde el archivo

```bash
conda env create -f environment.yml
conda activate redes
```

### Registrar el kernel para Jupyter

```bash
python -m ipykernel install --user --name redes --display-name "Python (redes)"
```

### Abrir los notebooks

```bash
jupyter lab
```

Despues, en Jupyter selecciona el kernel `Python (redes)`.

## Librerias base incluidas

- `networkx`
- `matplotlib`
- `numpy`
- `pandas`
- `ipykernel`
- `jupyterlab`

## Flujo sugerido

1. Clona el repositorio.
2. Crea el entorno con `environment.yml`.
3. Activa `redes`.
4. Abre `jupyter lab`.
5. Ejecuta los notebooks con el kernel `Python (redes)`.

## Validacion en GitHub

Se incluye una accion en `.github/workflows/validate-environment.yml` que reconstruye el entorno y corre un smoke test de imports en cada `push` y `pull request`.

