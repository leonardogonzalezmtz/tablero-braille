# Braille a través del juego

App para controlar un tablero Braille de seis botones grandes. Cada botón tiene una nota fija (1 Do, 2 Re, 3 Mi, 4 Fa, 5 Sol, 6 La) y un LED, y el tablero se conecta al celular por Bluetooth con un módulo HM-10. La app tiene cinco modos: piano libre, acción–reacción, aprendizaje guiado, memoria y personalizado con biblioteca de palabras.

Proyecto de Ingeniería en Mecatrónica del Tecnológico de Monterrey, Campus Querétaro, en colaboración con el CRIQ. Desarrollada con asistencia de IA.

## Archivos

- `index.html` es toda la app
- `manifest.webmanifest` y los íconos permiten instalarla en el celular
- `sw.js` guarda la app para que abra sin internet

## Publicar en GitHub Pages

1. Crear un repositorio público y subir estos archivos en la raíz.
2. En Settings → Pages elegir Deploy from a branch, rama `main` y carpeta `/ (root)`.
3. La app queda en `https://USUARIO.github.io/REPOSITORIO/`.

## Instalar en el celular

**Android:** abrir el link en Google Chrome y pulsar el botón Instalar app del encabezado, o en el menú ⋮ elegir Instalar app.

**iPhone:** instalar Bluefy desde la App Store y abrir el link desde ahí. Safari y Chrome en iPhone no permiten Bluetooth desde páginas web.

## Protocolo entre la app y el PIC

Cada comando es una línea de texto terminada en salto de línea, a 9600 baudios.

De la app al PIC:

- `M0` a `M5` cambia de modo (0 ninguno, 1 piano libre, 2 acción–reacción, 3 aprendizaje, 4 memoria, 5 personalizado)
- `L3,1` enciende el LED 3 y `L3,0` lo apaga
- `X` apaga todos los LEDs
- `N3` toca la nota del botón 3
- `S11` a `S37` reproduce la letra (11 es la a, 24 es la ñ y 37 es la z, en el orden a b c d e f g h i j k l m n ñ o p q r s t u v w x y z)
- `F1` correcto, `F2` intentar otra vez, `F3` actividad completada

Del PIC a la app:

- `B1` a `B6` se presionó ese botón
- `R` el tablero está listo

El PIC toca la nota de cada botón en cuanto se presiona, sin esperar a la app. Las palabras personalizadas las pronuncia el celular.

## Pistas sugeridas para el DFPlayer

En la microSD, dentro de una carpeta `mp3`, con nombres de cuatro dígitos para reproducirlas con el comando 18:

- `0001.mp3` a `0006.mp3` notas Do a La
- `0011.mp3` a `0037.mp3` letras
- `0051.mp3` correcto, `0052.mp3` intentar otra vez, `0053.mp3` completado
