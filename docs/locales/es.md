| [KR 한국어](./ko.md) | [US English](../../README.md) | [JP 日本語](./ja.md) | [CN 简体中文](./zh-CN.md) | [ES Español](./es.md) |
| :---: | :---: | :---: | :---: | :---: |
| [FR Français](./fr.md) | [DE Deutsch](./de.md) | [RU Русский](./ru.md) | [SA العربية](./ar.md) | [IN हिन्दी](./hi.md) |

---

# Johyo Jeun (`johyojeun-netizen`)

```text
       __      __               __                     
      / /___  / /_  __  ______ / /__  __  ______       
 __  / / __ \/ __ \/ / / / __ \/ / _ \/ / / / __ \      
/ /_/ / /_/ / / / / /_/ / /_/ / /  __/ /_/ / / / /      
\____/\____/_/ /_/\__, /\____/_/\___/\__,_/_/ /_/       
                 /____/                                 
 Ingeniero Senior de Sistemas y DSP de Audio en Tiempo Real · Seúl / Berlín
```

> "Estricta seguridad en tiempo real duro, fidelidad acústica matemática y modelado físico táctil del sonido."

Soy ingeniero de procesamiento digital de señales (DSP) de audio y desarrollador de sistemas, especializado en acústica espacial en tiempo real duro, renderizado psicoacústico binaural y síntesis de sonido por modelado físico. Mi trabajo principal se centra en el diseño de plugins de audio de latencia ultra baja (CLAP / VST3), cadenas de filtrado aceleradas por SIMD, entornos de ejecución embebidos para bare-metal y Linux, y algoritmos matemáticos abiertos para paisajes sonoros multicanal inmersivos.

Más allá del desarrollo de software comercial, construyo módulos de sintetizador Eurorack analógicos y digitales, realizo mediciones de respuesta al impulso (IR) en espacios arquitectónicos singulares y optimizo estructuras de búfer sin bloqueos (lock-free) para callbacks de audio sub-milisegundo.

---

## 🧭 Filosofía de Ingeniería

- **Seguridad Absoluta en el Hilo de Audio (Hard Real-Time)**: El callback de procesamiento de audio es sagrado. Cero asignaciones dinámicas en memoria (`malloc`/`new`), cero exclusiones mutuas (`mutex`), cero operaciones de I/O en disco o red, y cero primitivas de sincronización que puedan inducir inversión de prioridades o subejecución de búfer (xruns).
- **Modelado Físico Frente a Muestreo Estático**: En lugar de almacenar tablas estáticas PCM de decenas de gigabytes, resolvemos en tiempo real las ecuaciones diferenciales de onda continua de la materia física: cuerdas tensas no lineales, columnas de aire resonantes, membranas percutidas y reflexiones espaciales.
- **Procesamiento SIMD Orientado a Datos**: Diseño de las estructuras de búfer en formato Struct-of-Arrays (SoA) para aprovechar al máximo las instrucciones vectoriales AVX2 / AVX-512 y ARM NEON de 8 vías, procesando bloques contiguos de punto flotante en líneas de caché sin fallos en el predictor de saltos.
- **Estándares Abiertos y Grafos Modulares de Señal**: Apuesta decidida por arquitecturas abiertas como el formato de plugin CLAP, flujos flotantes IEEE de 32/64 bits no intercalados y motores modulares de grafos de nodos capaces de ejecutarse desde microcontroladores hasta estaciones de trabajo de audio digital (DAW) de alta densidad.

---

## 🛠️ Arsenal Técnico Principal

### Lenguajes de Programación y Entorno de Desarrollo

| Tecnología | Nivel de Dominio | Casos de Uso Principales |
| :--- | :--- | :--- |
| **C++ (C++20 / C++23)** | Producción Diaria | Motores de audio en tiempo real, algoritmos DSP, plugins CLAP/VST3, metaprogramación |
| **Rust** | Producción Diaria | Cadenas DSP seguras en memoria, búferes circulares lock-free, módulos WebAssembly |
| **C (C99 / C11)** | Nivel Avanzado | Microcontroladores embebidos, códecs de audio bare-metal, capas de abstracción hardware |
| **Zig** | Nivel Intermedio | Compilación cruzada, utilidades CLI de audio de alto rendimiento, runtimes mínimos |
| **Python** | Nivel Competente | Cálculo de coeficientes de filtrado, deconvolución de respuestas al impulso, simulación acústica |
| **POSIX Shell / Make / CMake** | Nivel Competente | Sistemas de compilación multiplataforma, ajuste del kernel Linux en tiempo real, pruebas de estrés |

### DSP, Acústica Espacial y Arquitectura de Audio

| Dominio | Áreas de Enfoque y Tecnologías Clave |
| :--- | :--- |
| **Acústica Espacial y HRTF** | Ambisonics de Alto Orden (HOA), convolución HRIR en formato SOFA, modelos de sombra esférica de cabeza |
| **Síntesis y Modelado Físico** | Mallas de Guía de Onda Digital (DWM), algoritmo Karplus-Strong, filtros de variables de estado no lineales |
| **Diseño de Filtros y Matemáticas Espectrales** | Remuestreadores polifásicos FIR/IIR, FFTW3 / pffft, transformada de Hilbert, feedback sin retardo (ZDF) |
| **Frameworks de Plugins de Audio** | API CLAP (Clever Audio Plugin), JUCE 8, SDK de VST3, WebAudio AudioWorklet |
| **Plataformas de Tiempo Real** | Optimización de kernel Linux RT-PREEMPT, ALSA / JACK / PipeWire, plataforma Bela, Teensy 4.1 |

---

## 🚀 Proyectos Destacados de Código Abierto

### 1. `reson-dsp` — Sintetizador Polifónico por Guías de Onda y Modelado Físico
- **Lenguaje**: C++23 / API CLAP
- **Descripción**: Motor de sonido polifónico que simula la resonancia acústica en barras metálicas golpeadas, campanas y cuerdas tensas mediante redes de guías de onda digitales bidimensionales.
- **Aspectos Destacados**:
  - Asignación determinista $O(1)$ de voces mediante colas circulares lock-free con capacidad acotada en tiempo de compilación.
  - Cero asignaciones dinámicas de memoria (cero `malloc`) durante todo el procesamiento de audio.
  - Cascada de filtros biquad vectorizados con AVX-512 y ARM NEON a 192 kHz con un consumo de CPU inferior al 2.8% en un solo núcleo.

### 2. `spatial-orb` — Espacializador 3D Binaural Ambisonics en Tiempo Real
- **Lenguaje**: Rust / WebAssembly
- **Descripción**: Motor de audio 3D que decodifica señales de Ambisonics de Alto Orden (hasta 5º orden HOA, 36 armónicos esféricos) hacia auriculares binaurales con perfiles HRTF personalizados.
- **Aspectos Destacados**:
  - Convolución rápida por bloques particionados (Overlap-Save) con latencia inferior a 1.2 ms.
  - Efecto Doppler paramétrico continuo y atenuación por distancia sin artefactos audibles de cremallera (zipper noise).
  - Compilación dual: binarios estáticos nativos (`.a` / `.so`) y módulos WebAssembly para integración en WebAudio AudioWorklet.

### 3. `wav-crunch` — Herramienta CLI de Análisis de Audio y Remuestreador Polifásico
- **Lenguaje**: Rust
- **Descripción**: Utilidad de consola de alta precisión sin dependencias externas para análisis a nivel de bit, detección de picos inter-muestra (True Peak mediante sobremuestreo 4x) y conversión de frecuencia de muestreo de fidelidad extrema.
- **Aspectos Destacados**:
  - Interpolación polifásica sinc con atenuación de ventana dinámica que supera los 144 dB de relación señal/ruido (SNR).
  - Procesamiento paralelo por lotes mediante grupos de subprocesos con balanceo dinámico de carga (work-stealing) alineados con la memoria caché.
  - Exportación integral de métricas de sonoridad LUFS (ITU-R BS.1770-4), rango dinámico y matrices de correlación de fase.

### 4. `patch-wire` — Entorno de Ejecución para Grafos Modulares de Señal de Audio
- **Lenguaje**: C++20 / C
- **Descripción**: Motor ligero de cálculo de señales de audio basado en grafos acíclicos dirigidos (DAG), optimizado para Linux embebido (Raspberry Pi CM4, Bela) y módulos digitales Eurorack autónomos.
- **Aspectos Destacados**:
  - Ordenación topológica calculada una sola vez en la fase de configuración; cero ramas condicionales en el bucle crítico del búfer de audio.
  - Huella de memoria estática y acotada: todo el grafo de nodos se aloja en un bloque contiguo de memoria alineado a la caché.
  - Sincronización precisa de voltajes de control CV/Gate mediante controladores de bus SPI e I2C en tiempo real.

---

## 📊 Arquitectura del Pipeline de Audio en Tiempo Real

```text
[ Controlador de Hardware de Audio (ALSA / ASIO / CoreAudio) ]
                             |
                             v (Interrupción / Callback)
+-------------------------------------------------------------------+
|               Callback en el Hilo de Audio de Tiempo Real         |
|                                                                   |
|   +-----------------------------------------------------------+   |
|   | 1. Ingesta de Entrada FIFO SPSC sin Bloqueo (Lock-Free)   |   |
|   +-----------------------------------------------------------+   |
|                                |                                  |
|   +-----------------------------------------------------------+   |
|   | 2. Procesamiento SIMD por Bloques (Filtros DSP / DWM)     |   |
|   |    - Bloques de 64 muestras                               |   |
|   |    - Registros vectoriales SoA (AVX-512 / NEON)           |   |
|   +-----------------------------------------------------------+   |
|                                |                                  |
|   +-----------------------------------------------------------+   |
|   | 3. Convolución Particionada HRTF Binaural                 |   |
|   |    - Búferes de solapamiento y conservación en tiempo     |   |
|   +-----------------------------------------------------------+   |
|                                |                                  |
|   +-----------------------------------------------------------+   |
|   | 4. Limitador de Saturación y Dither hacia Búfer DAC       |   |
|   +-----------------------------------------------------------+   |
+-------------------------------------------------------------------+
                             |
                             v
             [ DAC Físico / Salida de Auriculares ]
```

---

## ⏱️ Métricas de Latencia y Pruebas de Rendimiento

Mediciones realizadas en Linux 6.11 con parche `PREEMPT_RT`, en procesadores Intel Core i7-13700K (frecuencia fija a 4.8 GHz) y AMD Ryzen 9 7950X:

| Tamaño de Búfer | Frecuencia de Muestreo | Latencia de Entrada/Salida Falsa (I/O) | Tiempo Máximo por Bloque DSP | Conteo de xruns (24h de carga continua) |
| :---: | :---: | :---: | :---: | :---: |
| **32 muestras** | 96 kHz | **0.67 ms** | 18.4 µs | **0** |
| **64 muestras** | 96 kHz | **1.33 ms** | 34.2 µs | **0** |
| **128 muestras** | 192 kHz | **1.33 ms** | 56.8 µs | **0** |
| **256 muestras** | 48 kHz | **5.33 ms** | 41.1 µs | **0** |

---

## 🔬 Laboratorio de Acústica, Instrumentación y Estudio

| Categoría | Equipamiento y Herramientas |
| :--- | :--- |
| **Monitores y Auriculares de Referencia** | Monitores DSP Neumann KH 120 II, Sennheiser HD 800 S (curva EQ calibrada para campo difuso), Beyerdynamic DT 1990 Pro |
| **Medición Acústica Espacial** | Micrófono de referencia Earthworks M30, matriz tetraédrica Ambisonics de 1º y 2º orden, software REW |
| **Sintetizadores Hardware y Modular** | Sistema Eurorack 9U DIY personalizado (osciladores VCO analógicos, multiplicadores de onda Serge, DSP en Teensy) |
| **Instrumental de Diagnóstico Electrónico** | Osciloscopio digital Rigol DS1054Z de 4 canales, analizador lógico Saleae Logic Pro 8, analizador Audio Precision APx515 |
| **Bancos de Prueba de Audio Embebido** | Kit de desarrollo Bela Mini, Teensy 4.1 con Audio Shield rev D, Raspberry Pi CM4 con HiFiBerry DAC+ ADC Pro |

---

## 📬 Contacto y Colaboración

- **GitHub Issues y Discussions**: Canal preferido para reportes de errores, propuestas de diseño (RFC) y debates matemáticos sobre DSP.
- **Huella Digital PGP**: `4A8F B120 79E3 5DC6 D982 314F 88B1 C990 2A3E 761F`
- **Ubicación**: Seúl, República de Corea / Berlín, Alemania (UTC+9 / UTC+1)
- **Preferencia de Licencias**: Herramientas y algoritmos: Licencia MIT / Cabeceras de núcleo embebido: ISC o BSD-2-Clause
