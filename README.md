# Taller2-MLOPs

Todos los comandos se corren en PowerShell desde la **raíz del repo**.

## Ambiente virtual de Python (venv)

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
python --version
pip list
```

## Build del paquete `pipeline`

Con el venv activo:

```powershell
cd activity-01-sklearn-pipeline\pipeline_sklearn
pip install build
python -m build
cd ..\..
```

Genera `dist\*.whl` y `dist\*.tar.gz`. Ambos incluyen `pipeline/requirements-pipeline.txt` (wheel vía `[tool.setuptools.package-data]` en `pyproject.toml`, sdist vía `MANIFEST.in`). Una vez instalado el wheel, el archivo se lee con:

```powershell
python -c "from importlib.resources import files; print((files('pipeline') / 'requirements-pipeline.txt').read_text())"
```

## Ambiente Conda

Correr desde la **raíz del repo** (el `-r requirements.txt` de la sección `pip:` en `environment.yml` se resuelve relativo a esa carpeta):

```powershell
conda env create -f environment.yml
conda activate taller2-mlops
python --version
conda list
```

Si conda falla con `CondaToSNonInteractiveError` por los canales `defaults` (`repo.anaconda.com/pkgs/*`), hay que quitarlos del `.condarc` o aceptar sus términos:

```powershell
conda config --remove channels defaults
conda config --add channels conda-forge
```
