Lo ideal es trabajar con dependencias que sean compatibles con projectos de CMake, es decir, proyectos con CMakeLists.txt.

Si no se da el caso, como por ejemplo eon el proyecto `ffmpeg`, que funciona con el pipeline  clasico con makefiles, CMake incluye aun asi soluciones para poder integrar esa clas de proyectos externos.

En este articulo cubriremos tres metodologias populares para incluir proyectos externos en un flujo CMake.

## ExternalProject

External project es un modulo de CMake incluido por defecto con alta compatibilidad de versiones que permite envolver el proceso de compilacion de un proyecto no-cmake como una dependencia de pseudo target.

Para incluir modulos en cmake, podemos utilizar el comando `include`.

```cmake
# Nos deberia de proporcionar acceso a
# ExternalProject_Add
include(ExternalProject)

ExternalProject_Add(
  ffmpeg # pesudo target name
  SOURCE_DIR "${CMAKE_SOURCE_DIR}/lib/ffmpeg"
  CONFIGURE_COMMAND "./configure"
  BUILD_COMMAND "make -j $(nproc)"
)
```

Esta es la configuracion minima para `ExternalProject_Add`, a continuacion el significado de cada opcion:

1. `SOURCE_DIR`: Directorio del proyecto externo.
2. `CONFIGURE_COMMAND`:  Generacion de makefiles, por ejemplo `./configure`
3. `BUILD_COMMAND`: Compilacion desde makefiles, por ejemplo `make -j $(nproc)`.

---

## Flags de Compilacion no GPL FFMPEG

- --prefix: Indica la ruta base para instalaciones con `make install`.
- --enable-shared: Fundamental para componentes licenciados bajo LGPL
- --disable-static: Evita conflictos con la anterior opcion.
- --disable-programs: Solo compila librerias, no programas con main().
- --disable-doc: Tiempo de build mas rapido.
- --disable-libavdevice: Libreria para control avanzado de dispositivos de entrada / salida.
- --disable-swscale: Desactiva libreria de escalado de video y conversion de formatos de pixel.
- --disable-swresample: Permite modificar la tasa de frames. (ESTA SI LA NECESITAMOS).
- --disable-debug: No emitir simbolos de depuracion.
- --disable-gpl: No incluir componentes licenciados con GPL en los binarios finales.
- --disable-nonfree: Excluye todos los componentes no libres, es decir, no LGPL.
- --enable-avformat: Habilita libreria de identificacion de codecs, muxin / demuxin (LA NECESITAMOS).
- --enable-avcodec: Codificadores y Decodificadores. Hay muchos que sin libres, MP3 no esta incluido.
- --enable-avutil: Dependencia necesaria y requerida por el resto de librerias. Matematicas, manejo de buffers, y declaraciones.
- --enable-demuxer: Permite seleccionar que codecs son soportados para reducir el tamaño  de los binarios (NOS INTERESA CLARAMENTE)
- --enable-parser=mpegaudio: Habilita el parsing bit stream mp3 -> raw pcm.


## Miami
- --disable-postproc: Desactiva el postprocesado de video, que es licenciado con GPL. La cuestion es que no tiene mucho sentido y no se si es correcto incluirla si ya se indico la flag --disable-gpl.