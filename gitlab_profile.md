# GitLab Profile Configuration (gitlab.com)

## 1. Profile Settings (Settings -> Profile)

- **Full Name**: `Johyo Jeun` (또는 `조효준 / Johyo Jeun`)
- **Job Title**: `Senior Systems & Real-Time Audio DSP Engineer`
- **Bio** (248자 / 250자 제한):
  ```text
  Systems & audio DSP engineer in Seoul/Berlin. Focused on hard real-time audio threads, lock-free ring buffers, spatial HRTF convolution, and physical acoustic modeling. Building low-latency audio runtimes with C++23, Rust & Linux RT-PREEMPT.
  ```
- **Location**: `Seoul, South Korea · Berlin, Germany`
- **Website URL**: `https://github.com/johyojeun-netizen`

---

## 2. GitLab Profile README.md (`username/username` 저장소용)

```markdown
| [KR 한국어](https://github.com/johyojeun-netizen/johyojeun-netizen/blob/main/docs/locales/ko.md) | [US English](https://github.com/johyojeun-netizen/johyojeun-netizen/blob/main/README.md) | [JP 日本語](https://github.com/johyojeun-netizen/johyojeun-netizen/blob/main/docs/locales/ja.md) | [CN 简体中文](https://github.com/johyojeun-netizen/johyojeun-netizen/blob/main/docs/locales/zh-CN.md) | [ES Español](https://github.com/johyojeun-netizen/johyojeun-netizen/blob/main/docs/locales/es.md) |
| :---: | :---: | :---: | :---: | :---: |
| [FR Français](https://github.com/johyojeun-netizen/johyojeun-netizen/blob/main/docs/locales/fr.md) | [DE Deutsch](https://github.com/johyojeun-netizen/johyojeun-netizen/blob/main/docs/locales/de.md) | [RU Русский](https://github.com/johyojeun-netizen/johyojeun-netizen/blob/main/docs/locales/ru.md) | [SA العربية](https://github.com/johyojeun-netizen/johyojeun-netizen/blob/main/docs/locales/ar.md) | [IN हिन्दी](https://github.com/johyojeun-netizen/johyojeun-netizen/blob/main/docs/locales/hi.md) |

---

# Johyo Jeun (`johyojeun`)

```text
       __      __               __                     
      / /___  / /_  __  ______ / /__  __  ______       
 __  / / __ \/ __ \/ / / / __ \/ / _ \/ / / / __ \      
/ /_/ / /_/ / / / / /_/ / /_/ / /  __/ /_/ / / / /      
\____/\____/_/ /_/\__, /\____/_/\___/\__,_/_/ /_/       
                 /____/                                 
 Senior Systems & Real-Time DSP Engineer · Seoul / Berlin
```

> "Hard real-time audio guarantees, deterministic memory layouts, and continuous verification of acoustic DSP pipelines."

I am an audio digital signal processing (DSP) and low-level systems engineer. On GitLab, my primary focus is maintaining continuous verification pipelines and hardware-in-the-loop (HIL) testbeds for real-time audio systems: bit-exact regression testing, memory allocation detection in audio callbacks, SIMD cycle-accuracy verification across compiler revisions, and kernel preemption stress testing under Linux `PREEMPT_RT`.

---

## 🏗️ Active GitLab CI/CD Workstreams & Pipelines

| Workstream | Target / Stack | Focus Domain | Pipeline Mission |
| :--- | :--- | :--- | :--- |
| **`dsp-rt-guard`** | Linux 6.x `PREEMPT_RT` | Audio Callback Safety | Static and dynamic analysis verifying zero dynamic allocation (`malloc`/`new`), zero mutexes, and zero system calls inside hot audio processing loops. |
| **`simd-parity-matrix`** | GCC 14, Clang 18, Rust | Numerical Parity | Cross-compilation test matrix validating IEEE 754 bit-exact float output across AVX2, AVX-512, and ARM NEON vectorization backends. |
| **`alsa-jack-stress`** | ALSA, PipeWire, JACK2 | Hardware I/O Stress | Continuous 24-hour cyclic buffer under-run (xrun) endurance testing under extreme synthetic CPU and I/O pressure. |
| **`sofa-hrtf-validator`** | C++23, Python, SOFA | Spatial Acoustic Data | Deterministic validation of multi-channel HRTF impulse responses, checking reciprocity, causality, and phase linearity. |

---

## ⚙️ Core Technical Disciplines

```text
Languages:        C++ (C++20/C++23), Rust, C (C99/C11), Zig, Python, POSIX Shell
Audio Protocols:  CLAP API, VST3 SDK, WebAudio AudioWorklet, ALSA, JACK, PipeWire
Real-Time Linux:  PREEMPT_RT patchset, CPU core isolation (cset/taskset), IRQ thread pinning
Concurrency:      Lock-free SPSC/MPMC ring buffers, memory fences, atomic ordering
Vectorization:    AVX2, AVX-512 (FMA), ARM NEON, SoA (Struct-of-Arrays) buffer layouts
Verification:     Valgrind (Massif/Helgrind), AddressSanitizer, perf, flamegraphs
```

---

## 📐 Systems & Acoustic Invariants

1. **Zero-Allocation Audio Loops**: Every DSP filter cascade, waveguide mesh node, and delay line buffer must be statically provisioned or allocated at initialization time. Any runtime allocation during the audio callback fails CI builds immediately.
2. **Deterministic Round-Trip Latency**: Pipelines must reliably satisfy sub-1.5ms round-trip hardware I/O constraints at 96 kHz / 64-sample buffers without a single xrun.
3. **Bit-Exact Cross-Platform Reproducibility**: SIMD-optimized assembly routines must match canonical scalar double-precision reference implementations within strict $\epsilon \le 10^{-7}$ relative error thresholds.

---

## 📬 Connectivity & Mirrors

- **GitHub Profile**: [github.com/johyojeun-netizen](https://github.com/johyojeun-netizen)
- **Direct Mail**: `johyojeun@gmail.com`
- **PGP Fingerprint**: `4A8F B120 79E3 5DC6 D982 314F 88B1 C990 2A3E 761F`
```
