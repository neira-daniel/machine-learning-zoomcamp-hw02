# Tarea #2

Cuaderno de Jupyter con las soluciones.

[Enunciado](https://github.com/DataTalksClub/machine-learning-zoomcamp/blob/ba25a5e5b578ada996a573b64149279c88f4e9e2/cohorts/2025/02-regression/homework.md).

# Uso de Jupyter notebooks con `uv` en VS Code

## Requerimientos

- VS Code con la [extensión Jupyter](https://marketplace.visualstudio.com/items?itemName=ms-toolsai.jupyter) instalada
  - Es necesaria para poder interactuar con los cuadernos de Jupyter
  - Si está ausente, solo podremos visualizar los cuadernos
- [uv](https://docs.astral.sh/uv/)

## Documentación

- [Using Jupyter from VS Code](https://docs.astral.sh/uv/guides/integration/jupyter/#using-jupyter-from-vs-code) (astral.sh)
- [Jupyter Notebooks in VS Code](https://code.visualstudio.com/docs/datascience/jupyter-notebooks) (visualstudio.com)

## Flujo de trabajo

### En la terminal

Debemos preparar el entorno de trabajo del proyecto para poder trabajar con cuadernos de Jupyter en VS Code.

```bash
# inicializar `PROYECTO` en el directorio actual fijando la versión de Python deseada
uv init --app --python 3.13 PROYECTO
# ingresar al directorio que contiene el proyecto recién creado
cd PROYECTO
# instalar dependencias de ejecución
uv add numpy pandas seaborn
# instalar dependencias de desarrollo
# `ipykernel` es el kernel de IPython para Jupyter
# VS Code lo exige para poder trabajar con cuadernos de Jupyter en el entorno de `PROYECTO`
uv add --dev ipykernel
# abrir PROYECTO en VS Code
code .
```

### En VS Code

Una vez listo lo anterior, debemos configurar VS Code para trabajar con nuestro proyecto:

1. Seleccionar el intérprete de Python de nuestro proyecto:
   - `Ctrl-Shift-p > Python: Select Interpreter > Python Environments > .venv/bin/python`
1. Abrir un cuaderno de Jupyter o crear uno nuevo (`Ctrl-Shift-p > Create: New Jupyter Notebook`)

Esto debiera ser suficiente para poder comenzar a trabajar con el cuaderno de Jupyter en VS Code.

## Posibles problemas

### VS Code no puede acceder a los paquetes instalados en el proyecto

Algunas alternativas:

- Verificar que instalamos la extensión Jupyter
- Forzar una sincronización de las dependencias del proyecto y luego volver a abrir VS Code: `uv sync && code .`
- Activar el entorno de trabajo manualmente y luego volver a abrir VS Code:
  - `source .venv/bin/activate && code .` (deactivamos el entorno ejecutando `deactivate`)
- Arrancar un servidor de Jupyter local y conectarse a él con VS Code
  - Iniciar un servidor de Jupyter:
    - `uv run --with jupyter jupyter lab`
  - Conectarse al servidor con VS Code: [Connect to a remote Jupyter server](https://code.visualstudio.com/docs/datascience/jupyter-notebooks#_connect-to-a-remote-jupyter-server)

### No se pueden instalar paquetes desde el cuaderno de Jupyter

Siempre podremos instalar paquetes con una terminal que se esté ejecutando en la misma máquina que el servidor de Jupyter.

Si no pudiéramos acceder a una de esas terminales, la [solución específica para VS Code](https://docs.astral.sh/uv/guides/integration/jupyter/#using-jupyter-from-vs-code) que proponen los desarrolladores de `uv` es instalar `uv` como una dependencia de desarrollo: `uv add --dev uv`.
Luego deberíamos poder ejecutar comandos de `uv` precedidos por `!` dentro del cuaderno para que corran en el entorno de trabajo del proyecto.
Por ejemplo, `!uv add pydantic` agregará `pydantic` a las dependencias del proyecto.

Una solución que no depende de VS Code será crear un kernel siguiendo [estos pasos](https://docs.astral.sh/uv/guides/integration/jupyter/#creating-a-kernel).
Instalaremos luego paquetes desde el cuaderno de la misma forma recién descrita.
