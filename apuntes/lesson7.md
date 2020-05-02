### Optimización web

- [🎬 1. Optimización y peticiones desde cliente](https://youtu.be/dSzW3EJEqio)
- [🎬 2. Network en Chrome Dev Tools](https://youtu.be/LD1xEsajwKw)
- [🎬 3. Optimización de imágenes](https://youtu.be/SnLLr1KMTHc)
- [🎬 4. Optimización multimedia (audio/video)](https://youtu.be/oSy6GPwQXlc)
- [🎬 5. Explicación de la práctica](https://youtu.be/pGpEAKeW6J0)
- [📗 Slides](https://docs.google.com/presentation/d/1S6B_fibEJKUvxEhcsDnIKgTdw3PeA4j9BhidJcHB7dY/present)

#### Recursos

1. [Chrome Dev Tools](https://developers.google.com/web/tools/chrome-devtools)
2. [Network Chrome Dev Tools](https://developers.google.com/web/tools/chrome-devtools/network)
3. Optimización multimedia de imágenes
   - Formatos de imágenes
     - PNG: PNG8, PNG24
       - [OptiPNG](http://optipng.sourceforge.net/) + [AdvPNG](http://www.advancemame.it/doc-advpng.html) + [PNGout](http://advsys.net/ken/utils.htm)
     - JPG: WebP, JPG-XR, JPG2000
       - [mozjpeg](https://github.com/mozilla/mozjpeg) + [jpegtran](https://jpegclub.org/jpegtran/) + [jhead](https://www.sentex.ca/~mwandel/jhead/)
     - GIF: APNG
       - [GifSicle](https://github.com/kohler/gifsicle)
     - SVG
       - [SVG Pocket Guide](https://svgpocketguide.com/) + [SVGO](https://github.com/svg/svgo)
   - Conversión de imágenes
     - [ImageMagick](https://imagemagick.org/) + [convert CLI](https://imagemagick.org/script/convert.php)
4. Optimización multimedia de audio/video
   - Formatos de audio
     - MP3: [MPEG Layer III](https://www.iis.fraunhofer.de/en/ff/amm/consumer-electronics/mp3.html)
     - OGG: [Vorbis](https://xiph.org/vorbis/)
     - Opus: [Opus Codec](http://opus-codec.org/)
   - Formatos de video
     - MP4: [libx264](https://www.videolan.org/developers/x264.html)
     - HEVC: [libx265](http://x265.org/)
     - WebM: [WebMovie](https://www.webmproject.org/)
     - AV1: [AV1](https://aomedia.org/)
     - Otros: OGV: [Theora](https://theora.org/), MKV: [Matroska](https://matroska.org/)
   - Conversión de formatos
     - [ffmpeg](https://www.ffmpeg.org/)

#### Práctica

En esta práctica, lo que nos interesa es optimizar una página que se encuentre cargada de recursos utilizando algunas de las herramientas y recursos anteriores. El repositorio viene con una página web ya construída. Incluye varios assets entre los que se encuentran imágenes JPG, PNG, imágenes vectoriales SVG, videos y otros recursos que se muestran en la página.

El alumno tendrá que crear o generar algunos contenidos multimedia (imágenes, audios y videos) propios, añadirlos a la web y posteriormente, identificar sus datos y posteriormente optimizarlos. Recuerda que debes elaborar un `README.md` donde indicarás los pasos seguidos o los comandos utilizados para realizar las diferentes acciones que se piden en el guión.

A continuación se mencionan los puntos que el alumno debe hacer **como mínimo** para superar la práctica, pero puede optar por incluir más ficheros, trabajar en modificaciones adicionales y reflejarlas en el `README.md` (en un apartado **Modificaciones adicionales**), lo que será tomado positivamente en el momento de evaluar la práctica.

**FASE INICIAL DE LA PRÁCTICA**

1. Examina el código del fichero `index.js` y **modifica las primeras líneas**, en el objeto `SOCIAL`, con los nombres de usuario que utilizas en las redes diferentes sociales mencionadas. Esto hará que se actualice la web y los iconos sociales apunten a tu usuario de las diferentes redes. Opcionalmente, también puedes revisar el código HTML+CSS+JS para modificar estilos, añadir sección y detalles o añadir otros iconos de otras redes sociales para completar la página. Se utiliza [Font Awesome](https://fontawesome.com/) para los iconos.

2. El alumno deberá **crear un video** para colocar al final de la sección **Objetivo**. No será válido un enlace a Youtube/Vimeo u otra red, ya que debe ser un video alojado en nuestros assets, utilizando la etiqueta HTML `<video>`. Puedes grabar el video utilizando un programa como [OBS](https://obsproject.com/es), ya que en **fuentes** puedes añadir un "Dispositivo de captura de video" como una webcam y/o un "Captura de pantalla" para grabar lo que aparece en el monitor. Si lo prefieres y te resulta más sencillo, también puedes grabar el video con el móvil. La duración del video debe estar entre 30-60 segundos. La temática es libre, ¡sé original y divertido/a!

3. El alumno deberá **crear un audio** para colocar después del video anterior, utilizando la etiqueta HTML `<audio>`. Puedes grabar el audio utilizando el micro y un programa como [Audacity](https://www.audacityteam.org/). Si lo prefieres y te resulta más sencillo, también puedes grabar el audio con el móvil.

4. El alumno deberá **crear cuatro imágenes** y añadirlas a la galería de la sección **Galería**. Las dos primeras deberán ser **fotografías** (_puedes tomarlas con una cámara o el móvil_). Las dos últimas deberán ser **capturas de pantalla** del PC (_por ejemplo, del VSCode o GitHub donde estés trabajando_). Guardalas en un formato apropiado y añádelas a la web con un texto de pie de foto divertido. Recuerda que deberás modificar ligeramente el CSS de esa parte para que cambie el número de filas del grid.

5. Edita el fichero markdown llamado `REPORT.md`, donde rellenarás una **tabla comparativa** con todos los archivos de la página que se descargan al cargarla en el navegador. Puedes apoyarte en **Chrome Dev Tools** (pestaña Network) para saber cuales son esos archivos. Recuerda rellenar los campos apropiados para cada fichero, investigando que formato tienen, que tamaño que ocupan, que codecs están utilizando (en el caso de los videos/audios), etc...

_Nota_: Si las imágenes/videos las crean con el móvil, asegúrense de recuperarlas directamente. Si las envían a través de otros programas (Gmail, Redes sociales, etc...) a su equipo de trabajo, muchos de estos programas cambian el formato, bajan la resolución o reducen la calidad. Necesitamos un video con alta calidad para optimizarlo.

**FASE DE OPTIMIZACIÓN**

1. Utiliza `ffmpeg` para intentar optimizar el tamaño del audio. En este caso mantén la duración original, pero busca un códec diferente con el que consigas un tamaño más reducido y una calidad aceptable.

2. Utiliza `ffmpeg` para recortar el video y quedarte sólo con los 10-15 primeros segundos. Aprovecha y asignale el códec (audio/video) que consideres más apropiado de cara a la optimización. Refleja en el README por qué te has decantado por el codec elegido.

3. Utiliza las herramientas de optimización o estrategias que consideres oportunas para optimizar el resto de recursos de la página (JPEG, PNG, SVG, HTML, CSS, etc...). Refleja en el informe las particularidades para cada tipo de archivo. Ejemplo:

- **HTMLNANO**: Para los archivos HTML he utilizado el compresor `htmlnano` con la siguiente configuración: ....
- **OptiPNG**: Para los archivos PNG he utilizado el optimizador `optipng` con la siguiente configuración: ....

4. Despliega en GitHub Pages la versión final de la página con los recursos optimizados y escribe en el `README` un apartado de conclusión donde adjuntes una captura de pantalla del **Chrome Dev Tools** (Pestaña Network) indicando los valores que aparecen a pie de ventana:

- **Número de requests**: Número de recursos de la página web
- **MB transferidos**: Tamaño de todos los archivos descargados (comprimidos)
- **MB resources**: Tamaño de todos los archivos descargados (sin comprimir)
- **Finish**: Tiempo total que ha tardado en cargar todos los recursos (incluso peticiones extra).
- **DOMContentLoaded**: Tiempo total que ha tardado en procesar el HTML (DOM).
- **Load**: Tiempo total que ha tardado en cargar todos los recursos de la página (sin peticiones extra).

* **IMPORTANTE** Asegúrate de tener marcada la pestaña **Disable cache** en el Chrome Dev Tools.

#### Criterios importantes

- Creación de contenidos multimedia (audio+video+imágenes)
- Correcta construcción de la tabla `REPORT.md`
- Optimización detallada de imágenes
- Optimización detallada de video/audio
- Otras optimizaciones

#### Retos

1. Elige uno de los recursos (video, imagen, etc...) de tu página. Intenta optimizarlo con diferentes herramientas y formatos y haz una tabla comparativa para indicar cuál tiene los mejores resultados con ese archivo en cuestión.
