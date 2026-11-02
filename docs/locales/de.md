| [KR 한국어](./ko.md) | [US English](../../README.md) | [JP 日本語](./ja.md) | [CN 简体中文](./zh-CN.md) | [ES Español](./es.md) |
| :---: | :---: | :---: | :---: | :---: |
| [FR Français](./fr.md) | [DE Deutsch](./de.md) | [RU Русский](./ru.md) | [BR Português](./pt-BR.md) | [SA العربية](./ar.md) |

---

# Johyo Jeun (`johyojeun-netizen`)

```text
       __      __               __                     
      / /___  / /_  __  ______ / /__  __  ______       
 __  / / __ \/ __ \/ / / / __ \/ / _ \/ / / / __ \      
/ /_/ / /_/ / / / / /_/ / /_/ / /  __/ /_/ / / / /      
\____/\____/_/ /_/\__, /\____/_/\___/\__,_/_/ /_/       
                 /____/                                 
 Ingenieur für Raumakustik & Echtzeit-DSP · Seoul / Berlin
```

> "Strikte Hard-Realtime-Sicherheit, mathematische akustische Präzision und greifbare physikalische Klangmodellierung."

Ich bin Softwareentwickler und Ingenieur für digitale Audiosignalverarbeitung (DSP), spezialisiert auf deterministische Hard-Realtime-Raumakustik, binaurales psychoakustisches Rendering und physikalische Klangsynthese. Mein Schwerpunkt liegt auf der Entwicklung extrem latenzarmer Audio-Plugins (CLAP / VST3), SIMD-vektorisierter Filterketten, ressourcenschonender Audio-Laufzeitumgebungen für Bare-Metal und Linux-Systeme sowie quelloffener mathematischer Algorithmen für immersive Mehrkanal-Klangfelder.

Neben kommerziellen Audio-Plugins entwerfe ich analoge und digitale Eurorack-Synthesizermodule, vermesse Impulsantworten (IR) in resonanten architektonischen Räumen und optimiere lock-freie Pufferarchitekturen für Audio-Callbacks im Sub-Millisekundenbereich.

---

## 🧭 Technische Philosophie

- **Strikte Sicherheit im Audio-Thread (Hard Real-Time)**: Der Audio-Callback ist unantastbar. Keine dynamischen Speicherallokationen (`malloc`/`new`), keine Mutex-Sperren (`mutex`), keine Datei- oder Netzwerk-E/A und keinerlei Thread-Synchronisation, die Prioritätsinversionen oder Pufferunterläufe (xruns) auslösen könnte.
- **Physikalische Modellierung statt statischer Samples**: Anstatt gigabytelange statische PCM-Abtasttabellen abzuspielen, lösen wir kontinuierliche partielle Differentialgleichungen physikalischer Schwingungen in Echtzeit: nichtlineare Saitenspannungen, schwingende Luftsäulen, Membranen und Raumreflexionen.
- **Datenorientierte SIMD-Vektorisierung**: Anordnung der Audiopuffer im Struct-of-Arrays (SoA)-Format zur optimalen Ausnutzung von 8-fachen AVX2 / AVX-512- und ARM NEON-Vektorbefehlen. Gleitkomma-Audioblöcke werden ohne Verzweigungsfehler direkt in zusammenhängenden Cache-Zeilen verarbeitet.
- **Offene Standards und modulare Signalflussgraphen**: Konsequenter Einsatz zukunftssicherer Standards (CLAP-Pluginspezifikation, nicht verschachtelte IEEE 32/64-Bit-Gleitkommaströme) und leichtgewichtiger gerichteter azyklischer Graphen (DAG), die von Mikrocontrollern bis hin zu professionellen DAWs zuverlässig skalieren.

---

## 🛠️ Technisches Profil & Kernkompetenzen

### Programmiersprachen & Toolchains

| Technologie | Erfahrungsgrad | Hauptanwendungsbereiche |
| :--- | :--- | :--- |
| **C++ (C++20 / C++23)** | Tägliche Produktion | Echtzeit-Audio-Engines, DSP-Algorithmen, CLAP/VST3-Plugins, Template-Metaprogrammierung |
| **Rust** | Tägliche Produktion | Speichersichere DSP-Werkzeuge, sperrenfreie Ringpuffer, WebAssembly-Audiomodule |
| **C (C99 / C11)** | Fortgeschritten | Eingebettete Mikrocontroller, Bare-Metal-Audiocodecs, Hardware-Abstraktionsschichten |
| **Zig** | Mittelstufe | Cross-Compilation-Pipelines, eigenständige Audio-CLI-Werkzeuge, schlanke Runtimes |
| **Python** | Fundiert | Filterkoeffizienten-Berechnung, Deconvolution von Impulsantworten, akustische Modellierung |
| **POSIX Shell / Make / CMake** | Fundiert | Plattformübergreifende Build-Systeme, Echtzeit-Kernel-Konfiguration, automatische Benchmarks |

### Audio-DSP, Raumakustik & Systemarchitektur

| Fachgebiet | Forschungsschwerpunkte & Schlüsseltechnologien |
| :--- | :--- |
| **Raumakustik & HRTF** | Higher-Order Ambisonics (HOA), SOFA-Format HRIR-Faltung, sphärische Kopfschattenmodelle |
| **Synthese & Physikalische Modellierung** | Digitale Wellenleiternetzwerke (DWM), Karplus-Strong-Saitensynthese, nichtlineare Zustandsvariablenfilter |
| **Filterdesign & Spektralmathematik** | Polyphasen-FIR/IIR-Resampler, FFTW3 / pffft, Hilbert-Transformation, Zero-Delay Feedback (ZDF) |
| **Audio-Plugin-Frameworks** | CLAP (Clever Audio Plugin) API, JUCE 8, VST3 SDK, WebAudio AudioWorklet |
| **Echtzeit-Plattformen** | Linux RT-PREEMPT Kernel-Tuning, ALSA / JACK / PipeWire, Bela-Plattform, Teensy 4.1 |

---

## 🚀 Wichtige Open-Source-Projekte

### 1. `reson-dsp` — Sperrenfreier physikalischer Wellenleiter-Synthesizer
- **Programmiersprache**: C++23 / CLAP API
- **Projektbeschreibung**: Polyphone Echtzeit-Klang-Engine zur numerischen Modellierung akustischer Resonanzen in geschlagenen Metallstäben, Glocken und Saiten mittels zweidimensionaler digitaler Wellenleiterstrukturen.
- **Wichtigste Merkmale**:
  - Deterministische $O(1)$-Stimmzuweisung über zur Übersetzungszeit dimensionierte, sperrenfreie Ringpuffer.
  - Vollständiger Verzicht auf dynamische Speicherallokation (Zero Heap Allocation) während der Signalverarbeitung.
  - AVX-512- und ARM NEON-vektorisierte Biquad-Filterkaskaden mit unter 2.8% CPU-Last auf einem einzelnen Kern bei 192 kHz.

### 2. `spatial-orb` — Binauraler Echtzeit-Ambisonics-3D-Spatialisierer
- **Programmiersprache**: Rust / WebAssembly
- **Projektbeschreibung**: 3D-Audio-Engine zur Konvertierung mehrkanaliger Higher-Order Ambisonics (bis zur 5. Ordnung HOA, 36 Kugelflächenfunktionen) in ein binaurales Kopfhörersignal unter Nutzung individueller HRTF-Datensätze.
- **Wichtigste Merkmale**:
  - Partitionierte Overlap-Save-Schnellfaltung mit einer Gesamtlatenz von unter 1.2 ms.
  - Kontinuierlicher parametrischer Doppler-Effekt und entfernungsabhängige Pegelabnahme ohne störende Knack-Artefakte.
  - Duale Übersetzung: native statische Bibliotheken (`.a` / `.so`) und WebAssembly-Binärdateien für WebAudio AudioWorklet.

### 3. `wav-crunch` — SIMD 64-Bit Audioanalyse & Polyphasen-Resampler CLI
- **Programmiersprache**: Rust
- **Projektbeschreibung**: Eigenständiges Hochpräzisions-Kommandozeilenwerkzeug für bitgenaue Audioanalyse, Inter-Sample-Peak-Erkennung (True Peak durch 4-faches Oversampling) und verlustfreie Abtastratenkonvertierung.
- **Wichtigste Merkmale**:
  - Polyphasen-Sinc-Interpolation mit dynamischer Fensterfunktion für einen Signal-Rausch-Abstand (SNR) von über 144 dB.
  - Parallele Stapelverarbeitung mit Cache-ausgerichteten Work-Stealing-Thread-Pools.
  - Vollständiger Export von Lautheitsmesswerten nach ITU-R BS.1770-4 (LUFS), Dynamikumfang und Phasenkorrelationsmatrizen.

### 4. `patch-wire` — Mikromodulare Audio-Signalflussgraph-Laufzeitumgebung
- **Programmiersprache**: C++20 / C
- **Projektbeschreibung**: Schlanke, auf gerichteten azyklischen Graphen (DAG) basierende Audio-Signalverarbeitungs-Engine, optimiert für Embedded-Linux-Systeme (Raspberry Pi CM4, Bela) und autonome Eurorack-Digitalmodule.
- **Wichtigste Merkmale**:
  - Einmalige topologische Sortierung beim Graphaufbau; keinerlei bedingte Sprünge innerhalb der inneren Audio-Verarbeitungsschleife.
  - Streng begrenzter Speicherbedarf: Der gesamte Knotengraph liegt in einer einzigen, Cache-ausgerichteten Speicherarena.
  - Harte Taktsynchronisation für analoge CV/Gate-Steuerspannungen über echtzeitfähige SPI- und I2C-ADC-Treiber.

---

## 📊 Architektur der Echtzeit-Audiosignalverarbeitung

```text
[ Hardware-Audiotreiber (ALSA / ASIO / CoreAudio) ]
                        |
                        v (Hardware-Interrupt / Callback)
+-------------------------------------------------------------------+
|                     Echtzeit-Audio-Thread-Callback                |
|                                                                   |
|   +-----------------------------------------------------------+   |
|   | 1. Sperrenfreie SPSC-FIFO-Eingabeentnahme (Wartefrei)     |   |
|   +-----------------------------------------------------------+   |
|                               |                                   |
|   +-----------------------------------------------------------+   |
|   | 2. SIMD-Blockverarbeitung (DSP-Filter / DWM-Modellierung) |   |
|   |    - 64-Sample Pufferblöcke                               |   |
|   |    - SoA-Gleitkommaregister (AVX-512 / NEON)              |   |
|   +-----------------------------------------------------------+   |
|                               |                                   |
|   +-----------------------------------------------------------+   |
|   | 3. Binaurale HRTF-partitionierte Schnellfaltung           |   |
|   |    - Zeitbereichs-Overlap-Save-Puffer                     |   |
|   +-----------------------------------------------------------+   |
|                               |                                   |
|   +-----------------------------------------------------------+   |
|   | 4. Sättigungsbegrenzer & Dither in den DAC-Ausgangspuffer |   |
|   +-----------------------------------------------------------+   |
+-------------------------------------------------------------------+
                        |
                        v
          [ Physischer DAC / Kopfhörerausgang ]
```

---

## ⏱️ Ziel-Latenzen & Benchmark-Ergebnisse

Messwerte unter Linux-Kernel 6.11 mit `PREEMPT_RT`-Patch auf Intel Core i7-13700K (feste Taktfrequenz 4.8 GHz) und AMD Ryzen 9 7950X:

| Puffergröße | Abtastrate | Round-Trip-Latenz (Hardware-E/A) | Schlechtester Blockverarbeitungszeit | xrun-Zähler (24h Dauerlast) |
| :---: | :---: | :---: | :---: | :---: |
| **32 Samples** | 96 kHz | **0.67 ms** | 18.4 µs | **0** |
| **64 Samples** | 96 kHz | **1.33 ms** | 34.2 µs | **0** |
| **128 Samples** | 192 kHz | **1.33 ms** | 56.8 µs | **0** |
| **256 Samples** | 48 kHz | **5.33 ms** | 41.1 µs | **0** |

---

## 🔬 Akustikstudio & Hardware-Labor

| Kategorie | Geräte & Messinstrumente |
| :--- | :--- |
| **Abhöre & Referenzkopfhörer** | Neumann KH 120 II DSP-Studiomonitore, Sennheiser HD 800 S (Diffusfeld-entzerrt), Beyerdynamic DT 1990 Pro |
| **Akustische Messtechnik** | Kalibriertes Messmikrofon Earthworks M30, tetraedrische Ambisonics-Mikrofonarrays (1. und 2. Ordnung), REW |
| **Synthesizer & Modularsysteme** | Maßgeschneidertes 9U-Eurorack-System (analoge VCOs, Serge-Wellenmultiplizierer, eigene Teensy-DSP-Module) |
| **Elektronische Mess- & Debugwerkzeuge** | 4-Kanal-Digitaloszilloskop Rigol DS1054Z, Logikanalysator Saleae Logic Pro 8, Audio-Analysator Audio Precision APx515 |
| **Eingebettete Testplattformen** | Bela Mini Starter Kit, Teensy 4.1 Audio Shield rev D, Raspberry Pi Compute Module 4 mit HiFiBerry DAC+ ADC Pro |

---

## 📬 Kontakt & Zusammenarbeit

- **GitHub Issues & Discussions**: Bevorzugter Kommunikationsweg für Fehlermeldungen, Architekturvorschläge (RFCs) und signaltheoretische Diskussionen.
- **Code-Signatur & PGP-Fingerprint**: `4A8F B120 79E3 5DC6 D982 314F 88B1 C990 2A3E 761F`
- **Standorte**: Seoul, Republik Korea / Berlin, Deutschland (UTC+9 / UTC+1)
- **Lizenzierungsrichtlinie**: Werkzeuge & Algorithmen: MIT-Lizenz / Eingebettete Core-Header: ISC oder BSD-2-Clause
