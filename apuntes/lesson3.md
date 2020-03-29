### APIs de Javascript

- [🎬 1. APIs JS - Vibrate, Battery, Synth](https://youtu.be/YS6FebYdRVU)
- [🎬 2. APIs JS - Device, Gamepad, XHR/Fetch](https://youtu.be/rmerGA8UfbQ)
- [📗 Slides](https://docs.google.com/presentation/d/1DM8Isw64WktJ5U-aJ53NY0X8t_vlhJCHPLAwnfKdReM/present)
- [Previsualización de la práctica](practica-synth-voice.mp4)

#### Recursos

1. API Multimedia · [Soporte](https://caniuse.com/#feat=mdn-api_htmlmediaelement)
   - Mediante [HTMLMediaElement](https://developer.mozilla.org/es/docs/Web/API/HTMLMediaElement) (Enfoque nativo)
   - Mediante [HowlerJS](https://github.com/goldfire/howler.js/)
2. Vibrate API · [Soporte](https://caniuse.com/#feat=mdn-api_navigator_vibrate)
3. WebStorage (Local & Session) · [Soporte](https://caniuse.com/#feat=namevalue-storage)
4. Sintetizador de voz · [Soporte](https://caniuse.com/#feat=speech-synthesis)
5. Giroscopio y Acelerómetro · [Soporte](https://caniuse.com/#feat=deviceorientation)
6. Peticiones asíncronas
   - Mediante XHR · [Soporte](https://caniuse.com/#feat=xhr2)
   - Mediante Fetch · [Soporte](https://caniuse.com/#feat=fetch)
   - Mediante librería externa: [Axios](https://github.com/axios/axios)
7. Otras APIs interesantes
   - Batería · [Soporte](https://caniuse.com/#feat=battery-status)
   - PageVisibility · [Soporte](https://caniuse.com/#feat=pagevisibility)
   - Gamepad · [Soporte](https://caniuse.com/#feat=gamepad)
   - Payment Request · [Soporte](https://caniuse.com/#feat=payment-request)

#### Práctica Game Dialogue Synth

En la siguiente práctica, vamos a utilizar la API de síntesis de voz del navegador para construir un sistema simple de diálogos para un juego. El objetivo es crear varios perfiles de personajes, cada uno con sus propias características particulares. Se aconseja utilizar la siguiente organización:

- Una clase `Profile` para guardar las características del personaje, donde se pueden encontrar cosas como la velocidad de diálogo, el avatar del personaje o el color del texto. Por ejemplo:

```js
const manzProfile = new Profile("Manz", {
  lang: "es",
  rate: 2.0,
  pitch: 1.0,
  color: "#ff0000"
});
```

- Una clase `Conversation` para trabajar y controlar las conversaciones de todos los personajes. Una conversación se podría definir como un array de objetos, donde cada uno contiene la frase y el personaje que la pronuncia.

```js
const conversation = new Conversation(box);

conversation.addMessage([
  { author: manzProfile, text: "¡Hola a todos! ¿Qué tal están?" },
  { author: robotProfile, text: "Muy bien, ¡gracias!" },
  { author: breadmanProfile, text: "Yo también muy bien" },
  {
    author: manzProfile,
    text: "El robot habla con un acento un tanto raro..."
  },
  { author: robotProfile, text: "Es que soy del norte" }
]);
```

1. Implementa la clase `Profile` para definir las características del personaje.
2. Implementa la clase `Conversation` para definir la conversación global y su manejo del sintetizador de forma que sea ajeno a la página principal.
3. La forma más fácil de implementar el sistema de diálogos es haciendo que muestre cada frase de golpe. ¿Serías capaz de implementarla de forma que aparezca palabra a palabra, a medida que la pronuncia? (Pista: hay que usar eventos)
4. Separa en métodos de clase para que puedas decidir si utilizar el método `wordToWord()` para que el personaje muestre el texto palabra a palabra, o el método `letterToLetter()` para que muestre letra a letra, como en el juego **Undertale**. Implementa también un método para que reproduzca un sonido en cada letra. Puedes utilizar [Bxfr](https://www.bfxr.net/) (_requiere Flash/Adobe Air_) para generarlos.
5. Genera el `build` y haz el despliegue en GitHub Pages, de modo que se pueda ver el ejemplo en vivo.

#### Criterios importantes

- Web desplegada funcionando.
- Creación de varios perfiles diferentes
- Clase Profile
- Clase Conversation
- ¿Es capaz de mostrar el texto palabra a palabra?
- README

#### Retos

1. Implementa la API de vibración del navegador en tu ejemplo, para que vibre cada vez que un personaje pronuncie una palabra o frase. Ten muy en cuenta que la API de vibración sólo puedes comprobarla en [móviles o tablets](https://caniuse.com/#feat=mdn-api_navigator_vibrate) que lo soporten.

2. **Reto opcional**: Con el `localStorage` podríamos hacer que el navegador te solicite el nombre o nick de usuario y se guarde en el navegador, de modo que se guarde y lo recuerde incluso si cerramos el navegador y lo volvemos a abrir. ¿Sabrías implementar esta característica de modo que los personajes te llamen por tu nombre (si lo conocen) o por el nombre `Mr. Undefined` si no lo conocen?

3. Utilizando peticiones asíncronas podríamos externalizar objetos de nuestro código en ficheros JSON externos y ajenos a la lógica del proyecto. Intenta implementarlo con las opciones de configuración de los personajes.
