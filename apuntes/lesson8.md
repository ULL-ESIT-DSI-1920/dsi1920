### Docker

- [🎬 1. Introducción a Docker](https://youtu.be/PMTJyEkq8Zs)
- [🎬 2. Cliente CLI de Docker](https://youtu.be/1RV25SRUkY8)
- [🎬 3. Estados de contenedores y otros detalles](https://youtu.be/7DrTypToFGk)
- [🎬 4. Dockerfiles](https://youtu.be/xyOhKy5muv8)
- [🎬 5. Optimización de Dockerfiles](https://youtu.be/-hreXnr46D0)
- [🎬 6. Docker Compose](https://youtu.be/2ePxdarIPQc)
- [📗 Slides](https://docs.google.com/presentation/d/1eX10akWc9mzXWN0o_tP8weC4NMS1OkhLdyX-NN_VcvY/present)

_Nota:_ El tema 5 no es necesario para la práctica (no hay que optimizar las imágenes), pero comento algunos detalles que pueden venirles bastante bien y ayudarles en la práctica.

#### Recursos

1. Concepto de contenedores
   - [Docker](https://www.docker.com/)
   - [Instalación en Ubuntu](https://docs.docker.com/engine/install/ubuntu/)
   - [Docker: Getting Started](https://docs.docker.com/get-started/)
2. Nginx
   - [Servidor web: Nginx](https://nginx.org/)
   - [Nginx Beginner's Guide](http://nginx.org/en/docs/beginners_guide.html)
3. Docker Compose
   - [Docker Compose](https://docs.docker.com/compose/)

#### Práctica

Según Wikipedia, Docker es un proyecto de código abierto que **automatiza el despliegue** de aplicaciones **dentro de contenedores de software**, proporcionando una capa adicional de abstracción y automatización de virtualización de aplicaciones en múltiples sistemas operativos.

El objetivo de esta práctica es aprender el funcionamiento de Docker montando dos contenedores, que se crearán a partir de dos ficheros `Dockerfile` y uniéndolos a través de `Docker compose`. En el primero de ellos tendremos una aplicación Node (Backend) y en el segundo una web utilizando Parcel (Frontend).

Para ello, crearemos la siguiente estructura de ficheros y carpetas, que tendrá, entre otras cosas, los siguientes ficheros:

```
+ backend/                  Carpeta con la app node
      - server.js              Applicación node
      - data.json              Fichero de datos JSON
      - Dockerfile             Info para generar el contenedor de Docker
      - package.json           Info del proyecto backend
      - run.sh                 Script para crear el contenedor
+ frontend/                 Carpeta con la web con parcel
      - src/                   Carpeta con los ficheros fuente del front
      - Dockerfile             Info para generar el contenedor de Docker
      - nginx.conf             Configuración del servidor web Nginx
      - package.json           Info del proyecto frontend
      - run.sh                 Script para crear el contenedor
- docker-compose.yml        Fichero de Docker Compose (ver más adelante)
- run.sh                    Script para lanzar Docker Compose
```

##### 1) Crear la aplicación Node

El primer contenedor albergará una sencillísima aplicación `Node` en el fichero `server.js`, a la que instalaremos con `npm` la dependencia `express`. Dicha aplicación, escuchará y responderá dos peticiones:

1. Una petición `/` a la página principal, que devolverá la versión de la app:

```js
const PORT = 8081;
const HOST = "0.0.0.0";
const VERSION = "1.0";

const app = require("express")();

app.get("/", (req, res) => {
  res.send(`API VERSION ${VERSION}`);
});

app.listen(PORT, HOST);
console.log(`Running NODE on http://localhost:${PORT} (private)`);
```

- Una segunda petición a la ruta `/api`, que devolverá un JSON con información de los vengadores, incluidos en el fichero [data.json](data.json).

La idea es que al ejecutar `node server.js` deberíamos tener node escuchando peticiones tanto en `http://localhost:8081/` como en `http://localhost:8081/api/`.

##### 2) Dockerizar la aplicación Node

Ahora, nuestro objetivo es crear un contenedor con esta aplicación. Con esto podríamos tener `Node` en dicho contenedor y no necesitarlo en nuestro sistema anfitrión para hacer funcionar la aplicación.

Para ello, crearemos un fichero `Dockerfile` donde:

- Nos basaremos en la imagen de una de las últimas versiones de Node. Por ejemplo, la `12.12.0`.
- En el contenedor, trabajaremos en la carpeta `/app`, donde debemos copiar los ficheros necesarios de nuestro backend.
- Por último, ejecutar en el contenedor el comando `node server.js` para mantenerlo en escucha de peticiones.

Si todo esto funciona correctamente, deberiamos poder crear y ejecutar nuestro contenedor, y recibir las peticiones enviadas. No te olvides de crear un fichero `run.sh` con los comandos necesarios para construir la imagen de docker y ejecutar el contenedor basado en esa imagen.

##### 3) Crear nuestra web frontend

El segundo contenedor se albergará una sencilla web construída con Parcel como hemos hecho en anteriores prácticas. Utilizaremos la misma estructura y la crearemos como lo habíamos hecho anteriormente. A grandes rasgos deberemos tener:

- Un `index.html` con la estructura principal de la página.
- Un `css/index.css` con los estilos globales de la página.
- Un `js/index.js` con el código de nuestra web frontend.

En el último fichero, debemos realizar un `fetch` a la URL de la API de Node. Utilizando promesas, recuperaremos ese JSON e iremos recorriendo los datos para insertarlos en el DOM que iremos creando en cada iteración. La idea es mostrar una serie de «cartas» con la información de los personajes y el borde o fondo de la carta del color que se indica en la propiedad `color` del JSON del personaje.

##### 4) Dockerizar nuestro frontend

Al igual que hicimos con node, debemos crear un contenedor para almacenar nuestra web frontend. En este caso, deberemos crear una imagen multi-stage. Para ello, crearemos un `Dockerfile` donde:

- En el **primer stage**, copiaremos los archivos del proyecto, e instalaremos las dependencias de node que pudieramos tener (por ejemplo Howler o similares) y las globales (como parcel), y generaremos el build.
- Recuerda que Parcel se encuentra en fase alfa (ya que es una herramienta experimental). Puede que observes varios warnings en rojo en la fase de instalación.

- En el **segundo stage**, montaremos un servidor web como Nginx, que obtendrá el build del stage anterior y la pondrá en la carpeta del servidor web.
- Por último, arrancaremos el nginx para servir la web frontend.

##### 5) Configurar el servidor nginx

En el backend, `node` se encarga de escuchar las peticiones. En el frontend, aunque podríamos poner a Parcel a escuchar las peticiones (_como hemos hecho en los servidores de desarrollo locales de las prácticas anteriores_), no suele ser elegante para servidores en producción. Una forma más profesional es configurar un servidor `Nginx`, que es lo que vamos a hacer.

Para ello, vamos a sobreescribir el fichero `/etc/nginx/conf.d/default.conf` de la imagen de docker de Nginx. Ahí debe estar nuestra propia configuración, que será, como mínimo, la siguiente:

- Si el usuario pide la página principal (`/`), le enviará al `index.html` (frontend).
- Si el usuario pide la ruta `/api/`, le enviará a dicha ruta de node (backend).
- Si el usuario pide la ruta `/api/version/` , le enviará a la ruta `/` de node (backend).

No te olvides de crear un fichero `run.sh` con los comandos necesarios para construir la imagen de docker y ejecutar el contenedor basado en esa imagen.

Estas rutas no funcionarán hasta tener los 2 contenedores conectados, que haremos en el siguiente punto con `docker compose`.

##### 6) Unir frontend y backend con Docker Compose

Una vez tengamos ambos contenedores, nuestro objetivo será crear un fichero `docker-compose.yml` fuera de las carpetas `frontend` y `backend` para unir los dos contenedores anteriores. Para ello, debemos:

- Crear dos servicios (nginx y node).
- Unirlas por una misma red (app).
- Usaremos el puerto 80, para entrar directamente sin indicar el puerto explícitamente.

Hay que darse cuenta que estaremos creando una api pública, ya que el nginx está devolviendo la pagina principal desde la ruta principal `/`, pero está redireccionando al contenedor de node si pedimos `/api/` o `/api/version/`.

#### Resumen

En resumen, nuestra app debería cargar el frontend haciendo una petición a `/`, la cuál ejecutará el Javascript y hará un fetch a la ruta `/api/`, donde node devolverá el JSON con los datos y nuestro frontend lo procesará mostrándolo en la web. En un futuro, se podría reemplazar ese JSON por otro contenedor con una base de datos, que devuelva un JSON resultante de las consultas realizadas por API Rest o GraphQL, por ejemplo.

![Esquema Docker](esquema-docker.png)

#### Criterios importantes

El `README.md` deberá reflejar:

1. Lo que se hace en `server.js` (Node).
2. Lo que se hace en cada `Dockerfile` (Nginx y Node).
3. Lo que se hace en el `index.js` (Javascript).
4. Lo que se hace en `docker-compose.yml` (Docker-Compose).
5. Las peticiones disponibles (`/` y `/api/` como mínimo) y cualquier añadido extra/mejora.
