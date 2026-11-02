# Hugging Face Profile Configuration (huggingface.co)

## 1. Account Settings (Settings -> Profile)

- **Full Name**: `Johyo Jeun` (또는 `조효준 / Johyo Jeun`)
- **Bio** (Markdown 지원):
  ```text
  Senior Audio DSP & Systems Engineer. Researching mathematical wave mechanics, high-resolution spatial HRTF datasets (SOFA/AES69), and deterministic SIMD audio processing algorithms.
  ```
- **GitHub Username**: `johyojeun-netizen`
- **Homepage / Website**: `https://github.com/johyojeun-netizen`
- **Interests (Tags)**:
  - `audio-dsp`
  - `spatial-audio`
  - `acoustic-modeling`
  - `signal-processing`
  - `real-time-audio`

---

## 2. Hugging Face Profile Introduction Body (Overview & Portfolio)

```markdown
# Johyo Jeun (`johyojeun`)

**Senior Systems & Real-Time Audio DSP Engineer**  
Seoul, South Korea · Berlin, Germany

> *"Treating neural audio as an extension of mathematical wave physics: differentiable acoustic structures, continuous spherical HRTF fields, and zero-allocation CPU inference."*

I approach machine learning from the perspective of low-level audio digital signal processing (DSP) and wave physics. Rather than building opaque, unconstrained black-box models, my research explores physically grounded neural architectures: parameterizing differential wave equations, learning continuous Head-Related Transfer Functions (HRTF) across spherical coordinate spaces, and designing ultra-compact 1D convolutional neural audio operators that run in hard real-time on standard x86_64/ARM CPUs without GPU acceleration.

---

## 🔬 Research Focus in Acoustic Machine Learning

- **Differentiable Physical Waveguides**: Combining 2D digital waveguide mesh (DWM) equations with gradient descent to derive physical damping, tension, and boundary reflection coefficients from microphone recordings of acoustic resonant bodies.
- **Continuous-Field Spherical HRTF Representation**: Neural representations (SIREN / implicit neural representations) mapping continuous spherical coordinates $(\theta, \phi, r)$ to individualized binaural impulse responses, eliminating spatial interpolation artifacts in 5th-order Ambisonics decoding.
- **Sub-Millisecond Neural Audio Inference on CPU**: Hand-tuned int8 and float32 1D convolution kernels utilizing AVX-512 and ARM NEON instructions to execute neural audio filtering within a single 64-sample buffer block (< 1.33 ms at 96 kHz) with zero dynamic memory allocation.
- **High-Fidelity Acoustic Impulse Response Datasets**: Curating calibrated, anechoic-normalized spatial impulse response datasets recorded across architectural spaces, acoustic chambers, and physical resonant materials.

---

## 📦 Datasets, Models & Space Artifacts

| Artifact | Type | Stack | Description |
| :--- | :--- | :--- | :--- |
| **`sofa-spatial-binaural-kemar`** | Dataset | SOFA, Python, HDF5 | High-resolution dataset of 3D spatial Head-Related Impulse Responses (HRIR) normalized according to AES69-2022 standards for Ambisonics binaural rendering. |
| **`differentiable-waveguide-resonator`** | Model | PyTorch, C++23 LibTorch | Lightweight differentiable digital waveguide model that learns physical stiffness and boundary absorption parameters directly from audio waveforms. |
| **`simd-neural-biquad-worklet`** | Space / Demo | Rust, WebAssembly, WebAudio | Interactive browser demonstration of SIMD-accelerated vectorized neural biquad filter cascades running in a real-time AudioWorklet thread without audio dropouts. |

---

## 🛠️ Audio DSP & ML Toolchain

```text
Languages:     C++ (C++20/C++23), Rust, Python 3.11+, C (C99), WebAssembly
ML Frameworks: PyTorch, TorchScript, LibTorch (C++ inference runtime), ONNX Runtime
Audio/DSP:     JUCE 8, CLAP API, SOFA API, libsndfile, FFTW3 / pffft, scipy.signal
Vectorization: AVX-512, AVX2 (FMA), ARM NEON, SIMD intrinsics
Acoustic Lab:  Earthworks M30 measurement mic, Ambisonics tetrahedral arrays, REW
```

---

## 📬 Connectivity & Links

- **GitHub Profile**: [github.com/johyojeun-netizen](https://github.com/johyojeun-netizen)
- **GitLab Profile**: [gitlab.com/johyojeun](https://gitlab.com/johyojeun)
- **Direct Mail**: `johyojeun@gmail.com`
- **PGP Fingerprint**: `4A8F B120 79E3 5DC6 D982 314F 88B1 C990 2A3E 761F`
```
