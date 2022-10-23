
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
    - [Partes del protocolo HTTP](#partes-del-protocolo-http)
    - [Operations (Métodos)](#operations-métodos)
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

FastAPI también parado sobre los hombros de OpenAPI para generar documentación.

- [Open APIs](https://www.openapis.org/): es una especificación que define como describir, crear y visualzar API’s. Permite reconocer si una API está definida adecuadamente. Require de Swagger.

- [Swagger](https://swagger.io/): Es un framework para trabajar API’s.
- [ReDoc](https://redocly.com/) es un framework alternativo a Swagger, instalado por default con FastAPI.

FastAPI funciona sobre SwaggerUI (User Interface) que permite mostrar graficamente la API documentada. SwaggerUI obtiene especificaciones de Open API y la muestra por Fast API.

Swagger UI: http://127.0.0.1:8000/docs

![swagger-docs](https://imgur.com/QEyJ4xe.png)

ReDoc UI: http://127.0.0.1:8000/redoc

![redoc ui](https://imgur.com/u78SWZP.png)

## Desarmando el framework

> Nota: Los esquemas explicando los conceptos son del curso dado por [Facundo Garcia Martoni](https://twitter.com/facmartoni)

### Path Operations

**Path Operation: Es la combinación de una ruta acompañada de un método.**

Está dividido en dos partes:

- **Path/Routes/Endpoints**: Se le llama así a todos los elemento que agregamos a la derecha del dominio. (Tambien llamados endpoints)

- **Operations**: Es exactamente lo mismo que un método HTTP.

```python
@app.get("/") # Path Operator DECORATOR
def home(): # Path Operator FUNCTION
    return {"Hello": "World"}
```

![path-operations](https://imgur.com/AbgbEeV.png)

#### Partes del protocolo HTTP

- **Headers**: Son esquemas de `key: value` que contienen información sobre el HTTP request y el navegador. Aquí también se encuentran los datos de las cookies. La mayoría de los headers son opcionales.Como los headers HTTP son una parte fundamental de los mensajes entre clientes y servidores, el siguiente recurso puede ser util: [Headers del protocolo HTTP](https://diego.com.es/headers-del-protocolo-http)
- **Body**: Si se envía información al servidor a través de POST o PUT, esta va en el body.
- **Method**: Son operaciones que se pueden realizar mediante el protocolo.

#### Operations (Métodos)

[Métodos de petición HTTP by Mozilla](https://developer.mozilla.org/es/docs/Web/HTTP/Methods)

Los siguientes métodos son los mas utilizados:

- `GET`: El método `GET` solicita una representación de un recurso específico. Las peticiones que usan el método `GET` sólo deben recuperar datos.
- `POST`: El método `POST` se utiliza para enviar una entidad a un recurso en específico, causando a menudo un cambio en el estado o efectos secundarios en el servidor.
- `PUT`: El modo `PUT` reemplaza todas las representaciones actuales del recurso de destino con la carga útil de la petición.
- `DELETE`: El método `DELETE` borra un recurso en específico.

Los siguientes métodos son menos utilizados y mas complejos:

- `OPTIONS`: El método `OPTIONS` es empleado para describir las opciones de comunicación para el recurso de destino.
- `HEAD`: El método `HEAD` pide una respuesta idéntica a la de una petición GET, pero sin el cuerpo de la respuesta.
- `PATCH`: Para editar partes concretas de un recurso.
- `TRACE`: El método `TRACE` realiza una prueba de bucle de retorno de mensaje a lo largo de la ruta al recurso de destino.
- `CONNECT`: El método `CONNECT` establece un túnel hacia el servidor identificado por el recurso.

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