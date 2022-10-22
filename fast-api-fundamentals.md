
<div align="center">
    <h1>FastAPI: Fundamentos, Path Operations y Validaciones</h1>
    <img src="https://imgur.com/dA28QV8.png" width="">
</div>

- [Fundamentos de FastAPI](#fundamentos-de-fastapi)
  - [¿Qué es FastAPI?](#qué-es-fastapi)
  - [Frameworks que utiliza FastAPI por detrás](#frameworks-que-utiliza-fastapi-por-detrás)
  - [Hello World!](#hello-world)
  - [Documentación interactiva de una API](#documentación-interactiva-de-una-api)
- [Desarmando el framework](#desarmando-el-framework)
  - [Path Operations](#path-operations)
  - [Path Parameters](#path-parameters)
  - [Query Parameters](#query-parameters)
  - [Request Body y Response Body](#request-body-y-response-body)
  - [Models](#models)
- [Validaciones](#validaciones)
  - [Validaciones: Query Parameters](#validaciones-query-parameters)
  - [Validaciones: explorando más parameters](#validaciones-explorando-más-parameters)
  - [Validaciones: Path Parameters](#validaciones-path-parameters)
  - [Validaciones: Request Body](#validaciones-request-body)
  - [Validaciones: Models](#validaciones-models)
  - [Tipos de datos especiales](#tipos-de-datos-especiales)

## Fundamentos de FastAPI

### ¿Qué es FastAPI?

[FastAPI](https://fastapi.tiangolo.com/) es el framework mas veloz para el desarrollo web con Python. Enfocado para realizar APIs, es el mas rápido en lo que respecta a la velocidad del servidor compitiendo directamente con Node.Js o GO, considerados los lenguajes mas veloces para desarrollo de backend. 

Fue creado por [Sebastian Ramirez](https://twitter.com/tiangolo), es de código abierto y se encuentra en Github. Es usado por empresas como Uber, Windows, Netflix y Office.

### Frameworks que utiliza FastAPI por detrás

> FastAPI es framework que está parado, sobre los hombros de gigantes.

Los frameworks que utiliza son:

![frameworks-que-usa-fast-api-por-detras](https://imgur.com/YW14Abu.png)

- [Uvicorn](https://www.uvicorn.org/): es una librería de Python que funciona de servidor, es decir, permite que cualquier computadora se convierta en un servidor.
  - Un servidor puede ser:
    - Una computadora que distribuye tu aplicación.
    - Un paquete que convierta a tu computadora en esa computadora que distribuya tu aplicación.

- [Starlette](https://www.starlette.io/): es un framework de desarrollo web de bajo nivel, para desarrollar aplicaciones donde se requiere un amplio conocimiento de Python. FastAPI lo toma como base y se encarga de añadirle funcionalidades por encima para que se pueda usar mas fácilmente.

- [Pydantic](https://pydantic-docs.helpmanual.io/): Es un framework que permite trabajar con datos similar a pandas, pero este te permite usar modelos los cuales aprovechara FastAPI para crear la API.

### Hello World!

1. Creamos un entorno virtual para trabajar sobre el. (Hay documentacion, no lo explicaré)
2. Activamos entorno e instalamos fastapi:
   - Debemos instalar uvicorn tambien porque no se instala como dependencia de fastapi: `pip install fastapi uvicorn`
3. Creamos archivo main.py y creamos el hola mundo:

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def home():
    return {"Hello": "World"}
```

4. Uniciamos nuestro servidor desde una terminal con el comando: `uvicorn main:app --reload`
   - `uvicorn`: framework que crea el servidor.
   - `main:app`: Archivo que contiene nuestra app
   - `--reload`: Para que actualice el servidor automaticamente
5. Vamos a nuestro navegador y abrimos nuestro servidor en **127.0.0.1:8000**

### Documentación interactiva de una API

## Desarmando el framework

### Path Operations
### Path Parameters
### Query Parameters
### Request Body y Response Body
### Models

## Validaciones

### Validaciones: Query Parameters
### Validaciones: explorando más parameters
### Validaciones: Path Parameters
### Validaciones: Request Body
### Validaciones: Models
### Tipos de datos especiales