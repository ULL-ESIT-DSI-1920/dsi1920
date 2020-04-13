### Javascript + WebComponents

- [🎬 1. WebComponents: HTML Templates + Custom Elements](https://youtu.be/Uopb3qeezaI)
- [🎬 2. WebComponents: Shadow DOM + ES Imports](https://youtu.be/3yRY8N7iru0)
- [🎬 3. WebComponents: Ejemplo con Shadow DOM](https://youtu.be/oympiPQE5pc)
- [🎬 4. WebComponents: Otros detalles](https://youtu.be/9m63VCy9eew)
- [🎬 5. WebComponents: Explicación de la práctica](https://youtu.be/6aG9NQoN9qA)
- [🎬 6. WebComponents: Ejemplo práctico avanzado de WebComponents](https://youtu.be/U1xPFk4WO-U)
- [📗 Slides](https://docs.google.com/presentation/d/13_O1RjFO4FRtTO4gM1Q335zAZebj6mbmHBM3ixqP3mk/present)
- [Previsualización de la práctica](practica-mkart.mp4)

#### Recursos

1. Concepto de [componente](https://javascript.info/webcomponents-intro) (HTML+CSS+JS)
   - Explosión de frameworks
   - ¿Por qué usar componentes?
2. Enfoque nativo (WebComponents)
   - [HTML Templates](https://javascript.info/template-element)
   - [Custom Elements](https://javascript.info/custom-elements)
   - [Shadow DOM](https://javascript.info/shadow-dom)
   - [ES Modules](https://javascript.info/import-export)
   - [Slots](https://javascript.info/slots-composition)
3. CSS-in-JS
   - Filosofía y nacimiento del **CSS-in-JS**
   - Organización y globalidad: El «problema» de CSS
     - [BEM](http://getbem.com/): Metodología CSS
     - CSS Modules: [postcss-modules](https://github.com/css-modules/postcss-modules)
     - [ShadowDOM](https://developer.mozilla.org/en-US/docs/Web/Web_Components/Using_shadow_DOM)
4. Enfoque nativo de WebComponents con librerías
   - [lit-html](https://lit-html.polymer-project.org/), capa ligera de Google
   - [Atomico](https://atomico.gitbook.io/doc/), con Hooks React-style
   - [LitElement](https://lit-element.polymer-project.org/), basado en Clases
   - [LiteDOM](https://litedom.js.org/), basado en objetos
   - Otros: [StencilJS](https://stenciljs.com/), [Svelte](https://svelte.dev/), etc...

#### Práctica

En esta práctica vamos a crear una pequeña carrera de **Mario Kart**. Para ello, utilizaremos **WebComponents** para encapsular conceptos clave de la práctica, como los kart de cada personaje. De esta forma, podríamos crear un WebComponent llamado `KartPlayer`. Este componente es similar al concepto de **clases en programación** (de hecho, extiende de `HTMLElement`), y se recomienda que se vea como una extensión para crear una etiqueta HTML propia y personalizada a la que le daremos funcionalidad y apariencia.

La idea es que nuestra etiqueta HTML `<kart-player>` (o componente `KartPlayer`), incluya, maneje y controle datos del kart para encapsular su funcionamiento y hacernos más fácil y cómodo trabajar con él, sin que repercuta con el resto de la página. Cosas que podría controlar el componente podrían ser las siguientes:

- Incluir un nombre identificatorio del kart
- Incluir una imagen (asset) para representar visualmente el vehículo en la página. Usa el nombre `kart-personaje.png`, donde `personaje` es el nombre del mismo.
- Incluir los números de coordenadas del eje `x` y el eje `y` del kart en cuestión, para saber donde dibujarlo.
- Gestionar su código HTML y CSS asociado, en el interior del componente

Ten en cuenta que la idea es dibujar el kart en las coordenadas (x, y). A medida que avance la carrera, iremos aumentando el valor x y la carrera termina cuando llegue a **950** (_o el número definido como línea de meta_). Para esto, en la parte visual, nos podemos ayudar de la propiedad `transform: translate()` de CSS y utilizar custom properties (_variables CSS_) con `var(--nombre-variable)`.

1. La carrera debería tener un botón `Start` que comenzará la carrera hasta que uno de los Karts llegue a la meta (condición para terminar la carrera). Dicha condición podría ser cuando `x` sea `950`, por ejemplo.

2. Sería recomendable utilizar **ShadowDOM** para encapsular el HTML y CSS del componente y no afecte a otros karts. Una buena forma de organizarlo puede ser la siguiente (fragmento del componente `KartPlayer`):

```js
export class KartPlayer extends HTMLElement {
   ...

   get styles() {
   return `
      :host {
        position: absolute;
        display: inline-block;
        left: 0;
        top: ${this.y}px;
        transform: translateX(var(--x)) translateY(var(--y));
        transition: transform 0.25s;
        will-change: transform;
      }
      ...
    `;
   }

   render() {
      this.shadowRoot.innerHTML = `
         <style>${this.styles}</style>
         <item-kart></item-kart>
         <img src="${this.image}" alt="${this.name}">
       `;
   }
   ...
}
```

3. Sería interesante crear métodos de ayuda para el componente, que afecten al propio kart. Por ejemplo, una propuesta:

   - Un método `.inc()` que incrementa la cantidad que avanza el kart
   - Un método `.setSpeed()` que determina la velocidad que tomará el kart a partir de ese momento
   - Un método `.win()` y otro `.lose()` que establece el kart en cuestión como vencedor o perdedor (añadiendo alguna clase al HTML y activando algún efecto visual para destacarlo)
   - Un método `.isWinner()` que comprueba si un kart es un ganador.

4. En el archivo `index.js` principal se puede desarrollar la actividad general del juego. Se aconseja seguir un enfoque funcional, creando pequeñas funciones (_arrow functions_) que hagan tareas concretas. Por ejemplo:

   - `startRace()`
   - `endRace()`
   - `restartRace()`
   - `startIteration()`
   - etc...

5. La idea principal del juego es ejecutar una función (`startIteration()`) cada `1000 / 60` segundos (_aproximadamente, 60fps_), hasta que se cumpla un criterio específico que determine que ha finalizado el juego. Pista: Usar [timers](https://javascript.info/settimeout-setinterval).

Para abordar esta práctica, pueden utilizar la imagen que ha diseñado un usuario en DeviantArt, basándose en los del juego original de SNES. Lo ideal sería dividirlos en varias imágenes (deben haber 6 jugadores) de 128x128 de resolución, donde la imagen esté centrada y pegada a la parte inferior:

- Source: [Sprites Mario Kart](https://www.deviantart.com/snowgibbonbasilisk91/art/Super-Mario-Kart-Sprites-w-Customs-403971952)

#### Criterios importantes

- Aspecto visual y uso de imágenes (6 jugadores)
- Encapsulación con WebComponents
- Uso de ShadowDOM
- Uso de custom properties CSS (variables CSS)
- La carrera empieza y termina correctamente (detectando al ganador)

### Retos

1. Como reto opcional, se puede añadir la posiblidad aleatoria (`Math.random()`) de que en cada iteración, un kart obtenga un item. Si obtiene un plátano, la velocidad desciende a cero temporalmente, manteniendo el kart en el mismo sitio al resbalar con el plátano. Si obtiene un champiñón, la velocidad asciende temporalmente, haciendo que vaya más rápido durante un tiempo.

2. ¿Se te ocurre alguna funcionalidad extra para el juego? Impleméntala y documéntala en el README.
