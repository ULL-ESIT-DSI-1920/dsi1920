### Parcel + Scaffolding

- [🎬 Parcel + Scaffolding](https://www.youtube.com/watch?v=VQ6RfWG0aak)
- [📗 Slides](https://docs.google.com/presentation/d/1G-_eirr1j5iypgY643TjHswLdLFEovN9XB1o4KqbQTs/present)

### Recursos adicionales

- [🎬 Conceptos básicos HTML + CSS](https://youtu.be/epos-hGdwWM)

### Recursos

1. Servidores locales
   - [serve NPM package](https://www.npmjs.com/package/serve) · ~311K
   - [http-server NPM package](https://www.npmjs.com/package/http-server) · ~299K
   - [live-server NPM package](https://www.npmjs.com/package/live-server) · ~165K
   - [lite-server NPM package](https://www.npmjs.com/package/lite-server) · ~37K
   - [sirv NPM package](https://www.npmjs.com/package/sirv) · ~16K
   - [es-dev-server NPM package](https://www.npmjs.com/package/es-dev-server) · ~5K
   - [servor NPM package](https://www.npmjs.com/package/servor) · ~1K
2. ¿Qué son los automatizadores? ¿Qué es [Parcel](https://parceljs.org/)?
   - [Cómo empezar](https://en.parceljs.org/getting_started.html) con Parcel.
   - Scaffolding de un proyecto. Estructura de carpetas
3. Entorno de desarrollo y entorno de producción
   - Windows: [Git + Git Bash](https://gitforwindows.org/) o [WSL](https://docs.microsoft.com/es-es/windows/wsl/install-win10)
   - [GitHub Pages](https://pages.github.com/)
   - [gh-pages npm package](https://www.npmjs.com/package/gh-pages)
4. Opciones avanzadas de configuración de Parcel
   - [CLI](https://en.parceljs.org/cli.html)
   - [Recipes](https://en.parceljs.org/recipes.html)
5. Linters
   - [ESLint](https://eslint.org/): Linter de Javascript
   - [Prettier](https://prettier.io/): Formateador de código sin opinión
6. Parcel es una alternativa cómoda de...
   - [Webpack](https://webpack.js.org/): El más extendido (y complejo)
   - [Gulp](https://gulpjs.com/): Organizador y planificador de tareas
   - [Rollup](https://rollupjs.org/guide/en/): Enfoque muy utilizado para librerías JS.

#### Práctica

- [Enlace para crear la práctica](https://classroom.github.com/a/1B8YNT36)

En las siguientes prácticas y retos intentaremos abordar un enfoque híbrido donde trabajaremos tanto con tecnologías de frontend clásicas, tecnologías de backend (_como node_) o enfoque siguiendo la filosofía de devops. Para comenzar un proyecto, es muy importante tener una buena estructura de carpetas, una buena configuración y conocer bien todo el _scaffolding_ que hay detrás del mismo.

```
  nombre-del-proyecto
    |
    +-- dist
    +-- build
    +-- src
        |
        +-- css
        +-- js
        +-- assets
        |
        index.html
    +-- node_modules
    |
    package.json
    package-lock.json
    .gitignore
    README.md
```

> _Un ejemplo de estructura de carpetas de un proyecto_

El objetivo de esta práctica es tener un repositorio que siga las buenas prácticas vistas en clases, las cuales tendremos que utilizar de base para las siguientes prácticas que realizaremos. Por lo tanto, lo ideal sería practicar y configurar todo lo posible para trabajar cómodamente durante las siguientes semanas en nuestros proyectos.

1. Crea en tu **entorno de desarrollo** una buena estructura de carpetas para un futuro proyecto frontend. El documento `HTML` debe referenciar a un documento de estilos `CSS` y a un archivo `Javascript`, ambos con un contenido mínimo para comprobar que funcionan.

2. Inicializa correctamente tanto `Git` como `NPM` para tener nuestro proyecto bien configurado. No te olvides que, por norma general, `node_modules` nunca debería subirse a GitHub.

3. Instala **Parcel** y utilizalo como automatizador. ¿Debes instalarlo como paquete global o como paquete de proyecto? ¿Si lo instalasemos como paquete de proyecto que debemos tener en cuenta?

4. Revisa los scripts de NPM. Hay comandos que, posiblemente, sea mejor escribirlos ahí para evitar tener que escribir comandos largos. Crearemos un script `dev` o `start` que se encargará de lanzar el servidor local **Parcel** como desarrollo (_con hot reload_), otro script `build` que se encargará de crear la versión definitiva que irá en el **entorno de producción**. Por otro lado, también necesitaremos otro script `deploy` que subirá el contenido adecuado a **GitHub Pages**.

5. Instala y configura `ESLint` y `Prettier` para tu proyecto.

6. Escribe un buen `README.md` donde documentarás los pasos realizados para hacer esta práctica.

#### Criterios importantes

- Uso de una buena estructura de carpetas
- Uso de GIT/NPM
- Exclusión de `node_modules` (y otros) en GitHub
- Utilizacióno del automatizador Parcel
- Buena gestión de scripts de NPM
- Utilización de ESLint/Prettier
- Documentar la práctica en el `README.md`

#### Retos

Los siguientes retos pueden enfocarse como páginas individuales adicionales que pueden enlazarse desde la página HTML principal.

1. **Vinilo**: Crea un [disco de vinilo](https://es.wikipedia.org/wiki/Disco_de_vinilo) lo más realista posible haciendo uso de HTML y CSS. Intenta no utilizar imágenes. Esta parte la podremos utilizar de base para la próxima práctica. · [Previsualización de ejemplo](reto-vinyl.mp4)

2. **Assets con Parcel**: Investiga como importar assets (recursos estáticos) para utilizarlos en nuestra página con Parcel.
