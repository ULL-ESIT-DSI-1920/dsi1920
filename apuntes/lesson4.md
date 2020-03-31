### PostCSS

- [🎬 1. CSS: Especificidad y Preprocesadores](https://youtu.be/VQpRuQ2jh3M)
- [🎬 2. ¿Qué es PostCSS?](https://youtu.be/as7DK7Ls8t0)
- [🎬 3. Plugins para PostCSS](https://youtu.be/Qy25IKC3yXQ)
- [🎬 4. Resumen: Display CSS](https://youtu.be/H8Kpai551o8)
- [🎬 5. Flexbox CSS](https://youtu.be/1AyUbG7tIpM)
- [🎬 6. Grid CSS](https://youtu.be/HKU_3ydyk9U)
- [🎬 7. Custom Props + Gradientes](https://youtu.be/XPhuDmOzFo4)
- [🎬 8. Sombras CSS + Clip Path](https://youtu.be/5X4our9zBtE)
- [🎬 9. Transformaciones y animaciones CSS](https://youtu.be/7SNFkrsRMco)
- [📗 Slides](https://docs.google.com/presentation/d/1AAcV18yxbPTMo6VSGd4QviCVobXN6Osxo372IQEUwN4/present)
- [Previsualización de la práctica](apuntes/practica-pokedex.mp4)

#### Recursos

1. Introducción y repaso de CSS
   - [¿Qué es CSS?](../cheatsheets/css3-cheatsheet-lenguajecss.com.pdf)
   - Ejemplos básicos
2. ¿Qué son los preprocesadores?
   - [LESS](http://lesscss.org/): Preprocesador CSS
   - [Sass](https://sass-lang.com/): Preprocesador CSS
3. ¿Qué es PostCSS?
   - [PostCSS](https://postcss.org/)
   - El origen de PostCSS: [Autoprefixer](https://github.com/postcss/autoprefixer)
4. [Plugins de PostCSS](https://github.com/postcss/postcss/blob/master/docs/plugins.md)
   - Linter de CSS: [StyleLint](https://stylelint.io/)
   - Babel de CSS: [postcss-preset-env](https://preset-env.cssdb.org/)
     - [postcss-nesting](https://github.com/jonathantneal/postcss-nesting)
   - Autoimport de Google Fonts: [postcss-font-magician](https://github.com/jonathantneal/postcss-font-magician)
   - Minificador de CSS: [cssnano](https://cssnano.co/) o [postcss-clean](https://github.com/leodido/postcss-clean)
   - Eliminación de CSS no utilizado: [purgecss](https://github.com/FullHuman/purgecss/tree/master/packages/postcss-purgecss) o [uncss](https://github.com/uncss/postcss-uncss)
   - Framework [TailwindCSS](https://tailwindcss.com/)
5. Repaso rápido de [layouts en CSS](https://css-tricks.com/almanac/properties/d/display/)
   - Tipos básicos: **block**, **inline** e **inline-block**
   - Tipos flexibles: flex y inline-flex [Flexbox guide](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
   - Cuadrículas: grid y inline-grid [Grid guide](https://css-tricks.com/snippets/css/complete-guide-grid/)
6. CSS Moderno
   - [Custom Properties](https://developer.mozilla.org/es/docs/Web/CSS/Using_CSS_custom_properties) (Variables CSS)
   - [Viewport units](https://css-tricks.com/fun-viewport-units/)
   - [Gradientes](https://cssgradient.io/) y [sombras](https://neumorphism.io/)
   - Recortes con [clip-path](https://bennettfeely.com/clippy/)
   - [Transiciones](https://developer.mozilla.org/en-US/docs/Web/CSS/transition) y [Animaciones](https://developer.mozilla.org/en-US/docs/Web/CSS/animation)
   - [Transformaciones 2D/3D](https://developer.mozilla.org/en-US/docs/Web/CSS/transform)

#### Práctica

Necesitamos crear una **PokeDex** para mostrar un listado de los **151 pokémon de primera generación**. Para ello, podemos utilizar la API gratuita [PokeAPI](https://pokeapi.co/). Dicho servicio pone a nuestra disposición una API que al realizar la petición `https://pokeapi.co/api/v2/pokemon/1/` nos muestra información del pokémon **número 1**, que entre otras cosas que puedes profundizar en su [documentación](https://pokeapi.co/docs/v2.html), nos devuelve un JSON con la siguiente información:

```js
{
   abilities: [],     // Array de objetos con las habilidades del pokémon
   height: Integer,   // Altura del pokémon
   weigth: Integer,   // Peso del pokémon
   id: Integer,       // Número del pokémon en la pokedex
   moves: [],         // Movimientos del pokémon
   sprites: {},       // Imágenes del pokémon (frontal, trasera, shiny, etc...)
   stats: [],         // Estadísticas del pokémon
   types: [],         // Tipos del pokémon
   ...
}
```

Nuestro objetivo es realizar lo siguiente:

1. Crea una página donde se muestren todos los pokémon de la primera generación en un elemento HTML, donde en su interior aparezca la imagen del mismo, su ID y su nombre. Utiliza PostCSS para darle estilos y adaptarlos para que parezca una tarjeta o carta.

2. Modifica el ejemplo de modo que todos los pokemon se vean de espaldas y cuando pases el ratón por encima de ellos, se muestren de frente. ¿Serías capaz también de conseguir aumentar su tamaño mediante CSS? ¿Que propiedad tendrías que utilizar? ¿Encuentras alguna forma de mantener el pixelado de la imagen sin que se vea borrosa?

3. La forma más fácil de hacer los puntos anteriores es utilizar los recursos de forma local o teniendo un JSON en local con toda la información. Sin embargo, la idea de esta práctica es obtener la información desde la API de PokéAPI realizando peticiones desde Javascript y obteniendo la información necesaria. Asegúrate que lo estás haciendo así y comprueba que el orden de los pokémon es el correcto (ordenados, de menor a mayor). Pista: Las promesas y [`Promise.all()`](https://javascript.info/promise-api) podría ayudarte.

_NOTA:_ Ten en cuenta que la API de PokéAPI tiene un límite de 100 peticiones por IP al minuto (sin incluir las imágenes). Este es un caso didáctico para aprender a trabajar con promesas. Un buen criterio en el caso de que querer hacer algo real para poner en producción, podría ser almacenar la información en el localStorage del navegador (o en una base de datos en backend) y extraer los datos de allí, para no sobrepasar el límite de la API. De esta forma estaríamos usando esa capa como caché y las obtenemos de ahí si ya existen, evitando volver a hacer peticiones innecesarias.

#### Criterios importantes

- Mostrar cartas visuales con información
- Cambio visual del sprite (imagen) de espaldas al sprite de frente
- Obtención de información mediante la API PokéAPI
- ¿Los pokémon salen siempre en orden creciente?
- Mejoras o funcionalidades extra

#### Retos

1. Busca plugins de PostCSS que consideres interesantes y documentalos en el `README.md` con un enlace a su GitHub y una breve descripción de lo que hacen y para que podría serte útil.

2. **Digital Clock**: Reto fácil. Implementa un reloj digital que muestre la hora actual. Para conseguir el relleno izquierdo de los ceros, investiga el método [`.padStart()`](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/String/padStart).

3. **Analogic Clock**: Reto difícil. Implementa un reloj analógico que muestre la hora real · [Previsualización](reto-clock.mp4)
