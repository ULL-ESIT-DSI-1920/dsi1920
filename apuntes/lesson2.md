### Javascript ES2015+

- [🎬 1. JS2015+ - Introducción ES2015 + Babel](https://youtu.be/pT5lxMYWj6s)
- [🎬 2. JS2015+ - Conceptos básicos](https://youtu.be/_ogHw0vvTBU)
- [🎬 3. JS2015+ - Funciones y Módulos ES2015](https://youtu.be/Wsy5VXcDL_c)
- [🎬 4. JS2015+ - Trabajo con el DOM](https://youtu.be/iFhddZ5vUjU)
- [🎬 5. JS2015+ - API Multimedia + Spread + Timers](https://youtu.be/43UPKQAredw)
- [📗 Slides](https://docs.google.com/presentation/d/1l5ii2AAWgo-e9SglAk0cusC5G2RJvdEF58McFDf7lws/present)
- [Previsualización de la práctica](practica-jspotify.mp4)

#### Recursos

1. Ecosistema de clientes
   - Panorama de navegadores / Evergreen browsers
   - [Kangax: ECMAScript compatibility table](https://kangax.github.io/compat-table/es6/)
   - [CanIUse](https://caniuse.com/): ¿Se soporta esta característica?
2. ¿Qué es ECMAScript?
   - ECMAScript [2015/2016/2017/2018/2019](https://github.com/daumann/ECMAScript-new-features-list)
   - ¿Qué es [BabelJS](https://babeljs.io/)?
   - Características de ES2015+
     - [Let + Const](https://github.com/daumann/ECMAScript-new-features-list/blob/master/ES2015.MD#let--const)
     - [Arrow function](https://javascript.info/arrow-functions-basics) `() => { ... }`
     - [Classes](https://javascript.info/class)
     - [Template strings](https://javascript.info/string)
     - [Default + Rest + Spread](https://github.com/daumann/ECMAScript-new-features-list/blob/master/ES2015.MD#default--rest--spread)
     - [Destructuring](https://github.com/daumann/ECMAScript-new-features-list/blob/master/ES2015.MD#destructuring)
     - [Array functions](https://javascript.info/array-methods)
     - [Promises](https://javascript.info/promise-basics) + [Async/Await](https://javascript.info/async-await)
     - Módules
       - Sistema de [módulos antiguos](https://javascript.info/modules-intro): AMD, CommonJS, UMD
       - [Import/Export](https://javascript.info/import-export)
       - [Dynamic import()](https://javascript.info/modules-dynamic-imports)
3. Repaso rápido de HTML/DOM
   - Etiquetas [HTML5](https://codepen.io/manz/full/maVXvv)
   - [Selección del DOM](https://javascript.info/searching-elements-dom)
     - Vía clásica: `document.getElement*()`
     - Vía moderna: `document.querySelector*()`
   - [Manipulación del DOM](https://javascript.info/basic-dom-node-properties)
     - Vía high-level: `.textContent` e `.innerHTML`
     - Vía low-level: `.createElement()`
   - [Eventos](https://javascript.info/introduction-browser-events)
     - Vía simple: Desde HTML
     - Vía callbacks: `.onClick = f()`
     - Vía listeners: `.addEventListener()`

#### Práctica

Los automatizadores permiten trabajar con herramientas avanzadas en nuestros proyectos, de forma que sea más cómodo integrarlas en nuestro día a día. Como hemos visto en la práctica anterior, **Parcel** concretamente sigue un enfoque de **zero config**, o lo que es lo mismo, realiza mucha «magia» por debajo sin que nosotros seamos conscientes. Otros automatizadores como **WebPack**, **RollUp** o **Gulp** requieren un trabajo de configuración más laborioso.

Considera un documento HTML como el siguiente (_se incluye sólo el contenido de la etiqueta `<body>`_):

```html
<div class="item item-1 flex">
  <div class="cover"></div>
  <div class="vinyl flex">
    <div class="label flex">
      <div class="hole"></div>
    </div>
  </div>
</div>
```

En este fragmento de código, utilizamos ciertas clases siguiendo un enfoque denominado _Utility First_, donde los nombres de las clases representan una utilidad concreta. El mencionado HTML representa una capa `item` que contiene 2 elementos: `cover` y `vinyl`. El primero será la carátula de un vinilo de música, y el segundo el propio vinilo.

Asociando el siguiente CSS:

```css
.flex {
  display: flex;
  justify-content: center;
  align-items: center;
}

.cover {
  width: 200px;
  height: 200px;
  background: grey;
}

.vinyl {
  width: 200px;
  height: 200px;
  background: black;
  border-radius: 50%;
}
```

El objetivo de la práctica es crear una página **JavaSpotify** con varios vinilos que reproduzcan una canción cuando pulses sobre ellos.

1. Crea un proyecto con **Parcel** para trabajar con los fragmentos de código anteriores. Amplíalo lo que consideres necesario para adaptarlo a tu gusto. Se tomará en cuenta este esfuerzo a la hora de evaluar.

2. Busca varias canciones en formato MP3 y guárdalas en la carpeta `assets`. Puedes descargarlas desde [freepd.com](https://freepd.com/) o utilizar alguna que tengas. Haz lo mismo con varias imágenes para las carátulas de los vinilos. La forma más sencilla de hacer esto es metiendo un `<img>` dentro de la clase `cover`, aunque también puedes hacerlo desde CSS con la propiedad `background-image`. Vigila las proporciones de las imágenes para que sean cuadradas.

3. En la previsualización tienes el ejemplo mínimo a realizar, pero puedes ir investigando y añadiendo características para hacerlo más visual u organizar el contenido. Esto te permitirá adelantarte a temas que veremos un poco más adelante.

4. Recuerda ampliar el código HTML. Debes tener el mismo número de items en el HTML, que de imágenes de carátula y audios. Además, sería interesante incluir los siguientes estilos CSS:

```css
.vinyl {
  z-index: -1; /* Envía al vinilo al fondo (en eje Z) */
  transform: translateX(-200px); /* Mueve el vinilo detrás de la portada */
  transition: transform 0.5s; /* No realiza el movimiento de golpe */
}

/* Esto aplica CSS al vinilo que está a continuación (+) de una clase "open" */
.open + .vinyl {
  transform: translateX(-50px);
}
```

Esto hará que el vinilo se mueva cuando tenga la clase `open`. Ten en cuenta que en nuestro código Javascript, debemos añadir la clase `open` al `.cover` en el momento que nos interese. Puedes aprovechar y reutilizar parte del código del reto del vinilo para adaptarlo e incluirlo en la práctica para el esquema anterior.

4. Utilizando módulos de Javascript, crea dos clases `Player` y `Song` y expórtalas para utilizar en nuestro `index.js`, donde tendremos el siguiente hash o diccionario que tendremos que pasarle a la clase `Player`:

```js
const map = {
  ".item-1": "beat-thee",    // corresponderá a /src/assets/beat-thee.mp3
  ".item-2": "queen",        // corresponderá a /src/assets/queen.mp3
  ...
};
```

5. La clase `Player.js` debe analizar los ítems del `map` (_representan la clase HTML y el nombre del MP3 asociado_) uno por uno e instanciar una canción ( `Song` ).

6. La clase `Song.js` debe buscar en el DOM el elemento HTML indicado (_la clave del map_) y aplicarle un listener para reproducir la canción si se pulsa encima. Recuerda que con **Parcel**, podemos importar assets (**.mp3**, **.jpg**, etc...) de una carpeta y obtener un objeto (_hash o diccionario_) con una lista de pares clave-valor con el nombre del fichero y el fichero generado en `dist/`:

```js
import audios from "../assets/*.mp3";
// audios = { "beat-thee": "/beat-thee.a4721.mp3", ... }
```

- No es necesario controlar que sólo suene una canción a la vez.
- Es necesario controlar cada canción individualmente. Cuando se pulse en una canción que está siendo reproducida, se pausará. Cuando se vuelva a pulsar, se debe reanudar.

7. Asegúrate de estar utilizando `Prettier` (_recomendado_) y `ESLint` para revisar la calidad de tu código y corregir todos los errores. Añade un script `lint` en los scripts de NPM que revise el código y/o utiliza la extensión adecuada para verlo desde VSCode.

8. Publica en **GitHub Pages** la página generada y añade el enlace en la parte superior del repo o en el `README.md`. Para eso puedes usar el paquete `gh-pages` y hacer uso de `parcel build`. No te olvides de poner el nombre del repo al parámetro `--public-url` del `parcel build`.

9. No te olvides de documentar en el `README.md` cada uno de los pasos realizados para esta práctica.

#### Criterios importantes

1. Utilización de Parcel
2. Uso de assets (MP3)
3. Aspecto visual
4. Módulo Player.js
5. Módulo Song.js
6. Utilización de ESLint/Prettier
7. Funcionalidades extra

#### Retos

1. Revisa la API de audio y añade otras funcionalidades no mencionadas en la práctica. Puedes utilizar funcionalidades como la tasa de velocidad, volumen o eventos especiales para añadir funcionalidades concretas. No te olvides de documentarlas en el `README.md` y mencionarlo como **Funcionalidades extra**.

2. La librería `Howler.js` es una interesante librería que nos hace mucho más fácil trabajar con archivos de audio. ¿Serías capaz de cambiar tu proyecto y utilizar la librería `Howler.js`? ¿Cuál prefieres utilizar? ¿Por qué?

3. ¿Serías capaz de realizar esta práctica íntegramente desde Javascript? Es decir, crear la estructura HTML del interior del `<body>` directamente desde Javascript, haciendo uso de `document.body` y la creación de elementos en el DOM. Esto ayuda a comprender como funciona a bajo nivel el DOM de una página HTML y son unas bases interesantes si en el futuro quieres aprender como funcionan por debajo librerías como React y conceptos utilizados como **Virtual DOM**.
