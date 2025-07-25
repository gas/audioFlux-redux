

# audioFlux-redux


**audioFlux-redux** es una versión ligera y especializada de la librería `audioFlux`, diseñada para ofrecer un alto rendimiento en aplicaciones de Go a través de un *wrapper* de Cgo.

Esta versión elimina la gran mayoría de los algoritmos de la librería original para centrarse exclusivamente en dos funcionalidades clave, resultando en un binario más pequeño y una API mucho más sencilla de integrar.

-----

## Funcionalidades Conservadas

**`audioFlux-redux`** mantiene únicamente los módulos necesarios para dos tareas críticas en el análisis de audio musical en tiempo real:

### 1\. Análisis de Espectro de Alta Resolución (CQT)

Se ha conservado todo el motor de la **Transformada de Q Constante (CQT)**. A diferencia de una FFT estándar, la CQT proporciona una resolución de frecuencia logarítmica, ideal para el análisis musical, ya que ofrece una definición mucho mayor en las frecuencias graves.

  * **Caso de uso principal:** Alimentar un ecualizador de bandas reactivo y de amplio espectro que refleje con precisión la percepción del oído humano.
  * **Algoritmos incluidos:** `CQT`, `BFT` y todas sus dependencias de `FFT` y `filterbank`.

### 2\. Detección de Ritmo Rápida y Fiable (Onset)

Se mantiene el algoritmo de **detección de inicios (Onset)**, que es el componente fundamental para construir un detector de BPM (Beats Per Minute) robusto y eficiente. Este módulo identifica los "golpes" o eventos rítmicos en una señal de audio.

  * **Caso de uso principal:** Implementar un detector de BPM en tiempo real para aplicaciones musicales y de visualización.
  * **Algoritmos incluidos:** `Onset` y sus dependencias de análisis espectral.

-----

## Objetivo del Proyecto

El propósito de **`audioFlux-redux`** es servir como una dependencia C de alto rendimiento y bajo impacto para proyectos en Go que necesiten estas dos funcionalidades sin el peso y la complejidad de la librería `audioFlux` completa.

-----

## Licencia

Este proyecto derivado mantiene la licencia **MIT** original del proyecto `audioFlux`. Consulta el archivo `LICENSE.md` para más detalles.


## Documentation

Documentation of the original package can be found online:

[https://audioflux.top](https://audioflux.top/)

