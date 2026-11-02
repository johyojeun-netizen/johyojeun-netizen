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
 Engenheiro de Áudio Espacial & DSP em Tempo Real · Seul / Berlim
```

> "Rigor absoluto em tempo real rígido, fidelidade acústica matemática e modelagem física tangível do som."

Sou engenheiro de processamento digital de sinais (DSP) de áudio e desenvolvedor de sistemas, especializado em acústica espacial determinística em tempo real rígido, renderização psicoacústica binaural e síntese sonora por modelagem física. Meu trabalho principal concentra-se no desenvolvimento de plugins de áudio de latência ultra-baixa (CLAP / VST3), pipelines de filtragem acelerados por SIMD, ambientes de execução embarcados para bare-metal e Linux, e ferramentas matemáticas abertas para campos sonoros multicanais imersivos.

Além do desenvolvimento de software comercial, projeto módulos de sintetizadores Eurorack analógicos e digitais, realizo medições de resposta ao impulso (IR) em espaços arquitetônicos acusticamente singulares e pesquiso arquiteturas de buffers circulares livres de bloqueio (lock-free) para callbacks de áudio submilisegundo.

---

## 🧭 Filosofia de Engenharia

- **Segurança Rigorosa na Thread de Áudio (Hard Real-Time)**: O loop de callback de áudio é inviolável. Nenhuma alocação dinâmica de memória (`malloc`/`new`), nenhum bloqueio por exclusão mútua (`mutex`), nenhuma operação de E/S em disco ou rede, e nenhuma sincronização de threads capaz de induzir inversão de prioridade ou esvaziamento de buffer (xrun).
- **Modelagem Física Acima de Amostragem Estática**: Em vez de reproduzir tabelas de amostras estáticas PCM de dezenas de gigabytes, resolver em tempo real as equações diferenciais contínuas de ondas da matéria física: cordas tensas não lineares, colunas de ar ressonantes, membranas percutidas e reflexões acústicas do espaço.
- **Vetorização SIMD Orientada a Dados**: Estruturação dos buffers de áudio segundo o paradigma Struct-of-Arrays (SoA) para aproveitar instruções vetoriais AVX2 / AVX-512 e ARM NEON de 8 vias, processando blocos contíguos de ponto flutuante diretamente nas linhas de cache sem erros de previsão de desvio.
- **Padrões Abertos e Grafos Modulares de Sinal**: Compromisso com arquiteturas abertas como o padrão de plugins CLAP, fluxos de ponto flutuante IEEE 32/64 bits não intercalados e motores modulares de grafos acíclicos dirigidos (DAG) capazes de rodar desde microcontroladores até DAWs profissionais de alta densidade.

---

## 🛠️ Arsenal Técnico Principal

### Linguagens de Programação & Toolchains

| Tecnologia | Nível de Proficiência | Casos de Uso Primários |
| :--- | :--- | :--- |
| **C++ (C++20 / C++23)** | Produção Diária | Motores de áudio em tempo real, algoritmos DSP, plugins CLAP/VST3, metaprogramação |
| **Rust** | Produção Diária | Cadeias de ferramentas DSP seguras em memória, buffers circulares lock-free, WebAssembly |
| **C (C99 / C11)** | Nível Avançado | Microcontroladores embarcados, codecs de áudio bare-metal, camadas de abstração de hardware |
| **Zig** | Nível Intermediário | Compilação cruzada, utilitários CLI de áudio ultraleves, runtimes mínimos |
| **Python** | Nível Competente | Cálculo de coeficientes de filtro, deconvolução de respostas ao impulso, modelagem acústica |
| **POSIX Shell / Make / CMake** | Nível Competente | Sistemas de build multiplataforma, ajuste de kernel Linux em tempo real, testes automatizados |

### DSP, Acústica Espacial & Arquitetura de Áudio

| Domínio | Áreas de Pesquisa & Tecnologias-Chave |
| :--- | :--- |
| **Acústica Espacial & HRTF** | Ambisonics de Alta Ordem (HOA), convolução HRIR no formato SOFA, modelos de sombra esférica de cabeça |
| **Síntese & Modelagem Física** | Redes de Guias de Onda Digitais (DWM), síntese de cordas Karplus-Strong, filtros de variáveis de estado |
| **Design de Filtros & Matemática Espectral** | Reamostradores polifásicos FIR/IIR, FFTW3 / pffft, transformada de Hilbert, feedback sem atraso (ZDF) |
| **Frameworks de Plugins de Áudio** | API CLAP (Clever Audio Plugin), JUCE 8, SDK VST3, WebAudio AudioWorklet |
| **Plataformas de Tempo Real** | Otimização de kernel Linux RT-PREEMPT, ALSA / JACK / PipeWire, plataforma Bela, Teensy 4.1 |

---

## 🚀 Principais Projetos de Código Aberto

### 1. `reson-dsp` — Sintetizador Polifônico por Modelagem Física de Guias de Onda
- **Linguagem**: C++23 / API CLAP
- **Descrição**: Motor polifônico de modelagem física que simula a ressonância acústica de barras metálicas percutidas, sinos e cordas tensas não lineares através de redes bidimensionais de guias de onda digitais.
- **Destaques**:
  - Alocação determinística de vozes em $O(1)$ utilizando filas circulares lock-free com capacidade estritamente limitada em tempo de compilação.
  - Zero alocações dinâmicas na memória heap durante todo o ciclo de processamento de áudio.
  - Cascatas de filtros biquad vetorizados em AVX-512 e ARM NEON operando a 192 kHz com consumo inferior a 2.8% de CPU em um único núcleo.

### 2. `spatial-orb` — Espacializador 3D Binaural Ambisonics em Tempo Real
- **Linguagem**: Rust / WebAssembly
- **Descrição**: Processador de áudio 3D que decodifica sinais Ambisonics de Alta Ordem (até 5ª ordem HOA, 36 harmônicos esféricos) para fones de ouvido com perfis HRTF personalizados.
- **Destaques**:
  - Convolução rápida particionada (Overlap-Save) mantendo a latência abaixo de 1.2 ms.
  - Efeito Doppler paramétrico contínuo e atenuação por distância sem ruídos perceptíveis de chaveamento (zipper noise).
  - Compilação dual: bibliotecas estáticas nativas (`.a` / `.so`) e WebAssembly para integração com WebAudio AudioWorklet.

### 3. `wav-crunch` — Utilitário CLI de Análise de Áudio 64-bit & Reamostrador Polifásico
- **Linguagem**: Rust
- **Descrição**: Ferramenta em linha de comando de alta precisão e sem dependências externas para análise a nível de bit, detecção de picos interamostrais (True Peak via 4x oversampling) e conversão de taxa de amostragem de altíssima fidelidade.
- **Destaques**:
  - Interpolação polifásica sinc com janela dinâmica garantindo relação sinal-ruído (SNR) superior a 144 dB.
  - Processamento paralelo em lote com pool de threads do tipo work-stealing alinhado com linhas de cache.
  - Exportação completa de métricas de intensidade sonora LUFS (norma ITU-R BS.1770-4), faixa dinâmica e matrizes de correlação de fase.

### 4. `patch-wire` — Runtime para Grafos de Sinais Modulares de Áudio
- **Linguagem**: C++20 / C
- **Descrição**: Motor leve de processamento de sinal em grafos acíclicos dirigidos (DAG), otimizado para sistemas Linux embarcados (Raspberry Pi CM4, Bela) e módulos Eurorack digitais autônomos.
- **Destaques**:
  - Ordenação topológica executada uma única vez na configuração do grafo; zero desvios condicionais dentro do loop crítico do bloco de áudio.
  - Pegada de memória estática e delimitada: todo o grafo de nós reside em uma única arena contígua alinhada à cache.
  - Sincronização temporal estrita de tensões de controle analógicas CV/Gate através de drivers de barramento SPI e I2C em tempo real.

---

## 📊 Arquitetura do Pipeline de Áudio em Tempo Real

```text
[ Driver de Áudio de Hardware (ALSA / ASIO / CoreAudio) ]
                           |
                           v (Interrupção / Callback de Áudio)
+-------------------------------------------------------------------+
|               Callback da Thread de Áudio em Tempo Real           |
|                                                                   |
|   +-----------------------------------------------------------+   |
|   | 1. Consumo de Entrada FIFO SPSC Sem Bloqueio (Lock-Free)  |   |
|   +-----------------------------------------------------------+   |
|                               |                                   |
|   +-----------------------------------------------------------+   |
|   | 2. Processamento SIMD em Bloco (Filtros DSP / DWM)        |   |
|   |    - Blocos de 64 amostras                                |   |
|   |    - Registradores vetoriais SoA (AVX-512 / NEON)         |   |
|   +-----------------------------------------------------------+   |
|                               |                                   |
|   +-----------------------------------------------------------+   |
|   | 3. Convolução Rápida Particionada HRTF Binaural           |   |
|   |    - Buffers com preservação de sobreposição              |   |
|   +-----------------------------------------------------------+   |
|                               |                                   |
|   +-----------------------------------------------------------+   |
|   | 4. Limitador de Saturação & Dither para Buffer do DAC     |   |
|   +-----------------------------------------------------------+   |
+-------------------------------------------------------------------+
                           |
                           v
            [ DAC Físico / Saída de Fones ]
```

---

## ⏱️ Metas de Latência & Resultados de Benchmarks

Testes realizados sob o kernel Linux 6.11 com o patch `PREEMPT_RT`, em processadores Intel Core i7-13700K (frequência fixa em 4.8 GHz) e AMD Ryzen 9 7950X:

| Tamanho do Buffer | Taxa de Amostragem | Latência de Ida e Volta (I/O) | Pior Tempo de Processamento de Bloco DSP | Contagem de xruns (24h de carga contínua) |
| :---: | :---: | :---: | :---: | :---: |
| **32 amostras** | 96 kHz | **0.67 ms** | 18.4 µs | **0** |
| **64 amostras** | 96 kHz | **1.33 ms** | 34.2 µs | **0** |
| **128 amostras** | 192 kHz | **1.33 ms** | 56.8 µs | **0** |
| **256 amostras** | 48 kHz | **5.33 ms** | 41.1 µs | **0** |

---

## 🔬 Laboratório de Acústica, Instrumentação & Estúdio

| Categoria | Equipamentos & Ferramentas |
| :--- | :--- |
| **Monitores de Referência & Fones** | Monitores DSP Neumann KH 120 II, fones Sennheiser HD 800 S (curva EQ calibrada para campo difuso), Beyerdynamic DT 1990 Pro |
| **Medição Acústica Espacial** | Microfone de medição Earthworks M30, arranjos tetraédricos Ambisonics de 1ª e 2ª ordem, software REW |
| **Sintetizadores Hardware & Modular** | Sistema Eurorack 9U DIY personalizado (osciladores analógicos VCO, multiplicadores de onda Serge, DSP Teensy caseiro) |
| **Instrumentos de Diagnóstico Eletrônico** | Osciloscópio digital de 4 canais Rigol DS1054Z, analisador lógico Saleae Logic Pro 8, analisador Audio Precision APx515 |
| **Bancos de Teste Embarcados** | Kit de desenvolvimento Bela Mini, Teensy 4.1 com Audio Shield rev D, Raspberry Pi CM4 com HiFiBerry DAC+ ADC Pro |

---

## 📬 Contato & Colaboração

- **GitHub Issues & Discussions**: Canal prioritário para relatórios de bugs, propostas de evolução (RFCs) e debates matemáticos sobre DSP.
- **Impressão Digital PGP de Assinatura**: `4A8F B120 79E3 5DC6 D982 314F 88B1 C990 2A3E 761F`
- **Localização**: Seul, República da Coreia / Berlim, Alemanha (UTC+9 / UTC+1)
- **Preferência de Licenciamento**: Utilitários e algoritmos: Licença MIT / Cabeçalhos de núcleo embarcado: ISC ou BSD-2-Clause
