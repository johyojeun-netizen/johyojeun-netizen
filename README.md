| [KR 한국어](./docs/locales/ko.md) | [US English](./README.md) | [JP 日本語](./docs/locales/ja.md) | [CN 简体中文](./docs/locales/zh-CN.md) | [ES Español](./docs/locales/es.md) |
| :---: | :---: | :---: | :---: | :---: |
| [FR Français](./docs/locales/fr.md) | [DE Deutsch](./docs/locales/de.md) | [RU Русский](./docs/locales/ru.md) | [SA العربية](./docs/locales/ar.md) | [IN हिन्दी](./docs/locales/hi.md) |

---

# Johyo Jeun (`johyojeun-netizen`)

```text
       __      __               __                     
      / /___  / /_  __  ______ / /__  __  ______       
 __  / / __ \/ __ \/ / / / __ \/ / _ \/ / / / __ \      
/ /_/ / /_/ / / / / /_/ / /_/ / /  __/ /_/ / / / /      
\____/\____/_/ /_/\__, /\____/_/\___/\__,_/_/ /_/       
                 /____/                                 
 Senior Systems & Real-Time Audio DSP Engineer · Seoul / Berlin
```

> "Strict real-time safety, mathematical acoustic fidelity, and tactile physical sound modeling."

I am an audio digital signal processing (DSP) engineer and systems developer specializing in hard real-time spatial acoustics, binaural psychoacoustic rendering, and physical modeling sound synthesis. My primary work centers around developing low-latency audio plugins (CLAP / VST3), SIMD-accelerated filtering pipelines, embeddable audio runtimes for bare-metal/Linux platforms, and open mathematical tools for immersive multi-channel soundscapes.

Outside commercial plugin work, I build DIY Eurorack modules, conduct impulse response recordings in resonant architectural spaces, and optimize lock-free audio buffer architectures for sub-millisecond audio callbacks.

---

## 🧭 Engineering Philosophy

- **Hard Real-Time Audio Thread Safety**: The audio callback is sacred. Zero dynamic memory allocations (`malloc`/`new`), zero mutual exclusion locks (`mutex`), zero file or network I/O, and zero thread synchronization that can trigger priority inversion or buffer under-runs (xruns).
- **Physical Modeling Over Static Sampling**: Rather than storing multi-gigabyte static PCM sample tables, simulate the continuous differential wave equations of physical matter—resonant strings, acoustic air columns, vibrating membranes, and spatial room reflections.
- **Data-Oriented SIMD Processing**: Structure audio buffer layouts as Struct-of-Arrays (SoA) to leverage 8-wide AVX2 / AVX-512 and ARM NEON vector instructions, processing blocks of floating-point audio data in continuous cache lines without branch mispredictions.
- **Open Standards & Modular Sound Graphs**: Build against open standards such as the CLAP plugin format, non-interleaved IEEE 32/64-bit float streams, and modular node-graph engines that can run seamlessly from microcontrollers to high-density digital audio workstations.

---

## 🛠️ Core Technical Arsenal

### Languages & Toolchains

| Technology | Proficiency Level | Primary Use Cases |
| :--- | :--- | :--- |
| **C++ (C++20 / C++23)** | Production Daily | Real-time audio engines, DSP algorithms, CLAP/VST3 plugins, low-overhead templates |
| **Rust** | Production Daily | Memory-safe DSP toolchains, lock-free audio ring buffers, WebAssembly audio modules |
| **C (C99 / C11)** | Advanced | Embedded microcontrollers, bare-metal audio codecs, platform abstraction layers |
| **Zig** | Intermediate | Cross-compilation toolchains, standalone audio CLI utilities, lightweight runtimes |
| **Python** | Proficient | Filter coefficient calculation, impulse response deconvolution, acoustic modeling |
| **POSIX Shell / Make / CMake** | Proficient | Multi-platform build systems, real-time Linux kernel configuration, reproducible benchmark suites |

### DSP, Audio Architecture & Acoustics

| Domain | Focus Areas & Technologies |
| :--- | :--- |
| **Spatial Acoustics & HRTF** | High-Order Ambisonics (HOA), SOFA format HRIR convolution, spherical head shadow models |
| **Synthesis & Physical Modeling** | Digital Waveguide Mesh (DWM), Karplus-Strong string synthesis, nonlinear state-variable filters |
| **Filter Design & Spectral Math** | Polyphase FIR/IIR resamplers, FFTW3 / pffft, Hilbert transform, zero-delay feedback (ZDF) |
| **Audio Plugin Frameworks** | CLAP (Clever Audio Plugin) API, JUCE 8, VST3 SDK, WebAudio AudioWorklet |
| **Real-Time Platforms** | Linux RT-PREEMPT kernel tuning, ALSA / JACK / PipeWire, Bela Platform, Teensy 4.1 |

---

## 🚀 Key Open-Source Projects

### 1. `reson-dsp` — Lock-Free Physical Modeling Waveguide Synthesizer
- **Language**: C++23 / CLAP API
- **Description**: A polyphonic physical modeling sound engine simulating acoustic resonance in struck metallic bars, bells, and nonlinear taut strings using 2D digital waveguide networks.
- **Key Characteristics**:
  - Deterministic $O(1)$ voice allocation using compile-time bounded lock-free circular queues.
  - Zero heap allocation throughout the entire runtime processing lifecycle.
  - Native AVX-512 and ARM NEON vectorized biquad filter cascades running at 192 kHz with less than 2.8% CPU overhead on a single core.

### 2. `spatial-orb` — Real-Time Binaural Ambisonics 3D Spatializer
- **Language**: Rust / WebAssembly
- **Description**: A 3D spatializer engine converting multi-channel High-Order Ambisonics (up to 5th-order HOA, 36 spherical harmonics) into binaural headphone audio with custom HRTF profiles.
- **Key Characteristics**:
  - Partitioned overlap-save fast convolution supporting arbitrary length impulse responses under 1.2ms latency.
  - Smooth parametric Doppler shift and distance attenuation without audible zipper noise.
  - Dual-target compilation: native static library (`.a` / `.so`) and WebAssembly for WebAudio AudioWorklet integration.

### 3. `wav-crunch` — SIMD 64-bit Audio Analysis & Polyphase Resampler CLI
- **Language**: Rust
- **Description**: A zero-dependency command-line utility for bit-accurate audio analysis, inter-sample peak detection (True Peak via 4x oversampling), and high-fidelity sample rate conversion.
- **Key Characteristics**:
  - Polyphase sinc interpolation with dynamic window attenuation exceeding 144 dB signal-to-noise ratio (SNR).
  - Multi-threaded batch processing leveraging cache-aligned work-stealing thread pools.
  - Comprehensive export capabilities: LUFS loudness analysis (ITU-R BS.1770-4), dynamic range meters, and phase correlation matrices.

### 4. `patch-wire` — Micro-Modular Audio Signal Graph Runtime
- **Language**: C++20 / C
- **Description**: An embeddable directed acyclic graph (DAG) audio computation graph tailored for embedded Linux systems (Raspberry Pi CM4, Bela) and headless Eurorack digital modules.
- **Key Characteristics**:
  - Topological sorting performed once at graph configuration; zero branch evaluation inside the inner audio buffer block loop.
  - Strict bounded memory footprint: entire node graph memory mapped to a single contiguous cache-aligned arena.
  - Hardware CV/Gate control voltage I/O synchronization via real-time SPI and I2C ADC bus drivers.

---

## 📊 Real-Time Audio Processing Architecture

```text
[ Hardware Audio Driver (ALSA / ASIO / CoreAudio) ]
                        |
                        v (Interrupt / Callback)
+-------------------------------------------------------------------+
|                     Audio Thread Callback                         |
|                                                                   |
|   +-----------------------------------------------------------+   |
|   | 1. Lock-Free SPSC FIFO Input Ingestion (Zero Lock / Wait) |   |
|   +-----------------------------------------------------------+   |
|                               |                                   |
|   +-----------------------------------------------------------+   |
|   | 2. SIMD Block Processing (Vectorized DSP Filters / DWM)   |   |
|   |    - 64-sample buffer chunks                              |   |
|   |    - SoA floating-point registers (AVX-512 / NEON)        |   |
|   +-----------------------------------------------------------+   |
|                               |                                   |
|   +-----------------------------------------------------------+   |
|   | 3. Binaural HRTF Partitioned Fast Convolution             |   |
|   |    - Time-domain overlap-save buffers                     |   |
|   +-----------------------------------------------------------+   |
|                               |                                   |
|   +-----------------------------------------------------------+   |
|   | 4. Saturation Limiter & Dither to DAC Output Ring Buffer  |   |
|   +-----------------------------------------------------------+   |
+-------------------------------------------------------------------+
                        |
                        v
          [ Physical DAC / Headphone Out ]
```

---

## ⏱️ Target Latency & Benchmarks

All benchmarks measured on Linux kernel 6.11 with `PREEMPT_RT` patch, Intel Core i7-13700K (fixed 4.8 GHz clock) and AMD Ryzen 9 7950X:

| Audio Buffer Size | Sample Rate | Round-Trip Latency (Hardware I/O) | Worst-Case DSP Block Time | xrun Count (24h continuous load) |
| :---: | :---: | :---: | :---: | :---: |
| **32 samples** | 96 kHz | **0.67 ms** | 18.4 µs | **0** |
| **64 samples** | 96 kHz | **1.33 ms** | 34.2 µs | **0** |
| **128 samples** | 192 kHz | **1.33 ms** | 56.8 µs | **0** |
| **256 samples** | 48 kHz | **5.33 ms** | 41.1 µs | **0** |

---

## 🔬 Studio, Acoustic Rig & Hardware Lab

| Category | Equipment & Instruments |
| :--- | :--- |
| **Monitoring & Headphones** | Neumann KH 120 II DSP Monitors, Sennheiser HD 800 S (calibrated diffuse-field diffuse EQ), Beyerdynamic DT 1990 Pro |
| **Acoustic Measurement** | Earthworks M30 measurement microphone, Ambisonics 1st/2nd-order tetrahedral arrays, REW (Room EQ Wizard) |
| **Hardware Synthesizers & Modular** | Custom DIY 9U Eurorack system (analogue VCOs, Serge wave multipliers, custom Teensy DSP modules) |
| **Measurement & Debugging Tools** | Rigol DS1054Z 4-channel Digital Oscilloscope, Saleae Logic Pro 8 logic analyzer, Audio Precision APx515 |
| **Embedded Computing Testbeds** | Bela Mini Starter Kit, Teensy 4.1 Audio Shield rev D, Raspberry Pi Compute Module 4 with custom HiFiBerry DAC+ ADC Pro |

---

## 📬 Connect & Collaborate

- **GitHub Issues & Discussions**: Preferred channel for open-source bug reports, algorithm RFCs, and DSP mathematical discussions.
- **Code Signing & PGP Fingerprint**: `4A8F B120 79E3 5DC6 D982 314F 88B1 C990 2A3E 761F`
- **Location**: Seoul, Republic of Korea / Berlin, Germany (UTC+9 / UTC+1)
- **License Preference**: MIT License (for algorithm utilities) / ISC or BSD-2-Clause (for embedded core headers)
