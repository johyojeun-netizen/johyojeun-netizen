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
 Ingénieur Senior Systèmes & DSP Audio Temps Réel · Séoul / Berlin
```

> "Sécurité stricte en temps réel dur, fidélité acoustique mathématique et modélisation physique tactile du son."

Je suis ingénieur en traitement numérique du signal (DSP) audio et développeur de systèmes bas niveau, spécialisé dans l'acoustique spatiale en temps réel dur, le rendu psychoacoustique binaural et la synthèse sonore par modélisation physique. Mes travaux portent principalement sur la conception de greffons audio (plugins CLAP / VST3) à latence ultra-faible, de pipelines de filtrage vectorisés par SIMD, d'environnements d'exécution embarqués pour plateformes bare-metal et Linux, ainsi que d'outils mathématiques ouverts pour la spatialisation multicanale immersive.

En parallèle de mes activités logicielles, je conçois des modules de synthétiseur Eurorack analogiques et numériques, réalise des mesures de réponse impulsionnelle (IR) dans des architectures acoustiques résonantes, et optimise des structures de mémoires tampons sans verrou (lock-free) pour des rappels audio sous la milliseconde.

---

## 🧭 Philosophie d'Ingénierie

- **Sécurité Absolue du Thread Audio (Hard Real-Time)** : La boucle de rappel audio est inviolable. Zéro allocation dynamique en mémoire (`malloc`/`new`), zéro exclusion mutuelle (`mutex`), zéro entrée/sortie sur disque ou réseau, et aucune synchronisation de threads susceptible de provoquer une inversion de priorité ou un décrochage de tampon (xrun).
- **Modélisation Physique Contre Échantillonnage Statique** : Plutôt que de stocker des tables d'échantillons PCM statiques de plusieurs gigaoctets, simuler en continu les équations différentielles de propagation d'ondes de la matière physique : cordes en tension non linéaire, colonnes d'air en résonance, membranes élastiques et réflexions acoustiques spatiales.
- **Traitement Vectoriel SIMD Orienté Données** : Structuration des mémoires tampons selon le paradigme SoA (Struct-of-Arrays) pour exploiter les registres vectoriels AVX2 / AVX-512 et ARM NEON sur 8 voies, calculant des blocs contigus de nombres flottants en ligne de cache sans défaut de prédiction de branchement.
- **Standards Ouverts et Graphes Modulaires de Traitement** : Adoption résolue de standards ouverts (spécification CLAP, flux flottants IEEE 32/64 bits non entrelacés) et de moteurs de graphes orientés acycliques (DAG) exécutables aussi bien sur microcontrôleur que dans les stations audionumériques (DAW) professionnelles.

---

## 🛠️ Arsenal Technique Principal

### Langages de Programmation et Chaînes de Compilation

| Technologie | Niveau de Maîtrise | Cas d'Usage Principaux |
| :--- | :--- | :--- |
| **C++ (C++20 / C++23)** | Production Quotidienne | Moteurs audio temps réel, algorithmes DSP, plugins CLAP/VST3, métaprogrammation |
| **Rust** | Production Quotidienne | Chaînes d'outils DSP sûres en mémoire, tampons circulaires sans verrou, WebAssembly |
| **C (C99 / C11)** | Niveau Avancé | Microcontrôleurs embarqués, codecs audio bare-metal, couches d'abstraction matérielle |
| **Zig** | Niveau Intermédiaire | Compilation croisée, utilitaires CLI audio ultra-légers, environnements minimaux |
| **Python** | Niveau Confirmé | Calcul de coefficients de filtres, déconvolution de réponses impulsionnelles, modélisation |
| **POSIX Shell / Make / CMake** | Niveau Confirmé | Systèmes de compilation multiplateforme, optimisation de noyau Linux temps réel |

### DSP, Acoustique Spatiale et Architecture Audio

| Domaine | Domaines de Recherche et Technologies Clés |
| :--- | :--- |
| **Acoustique Spatiale & HRTF** | Ambisonie d'ordre élevé (HOA), convolution HRIR au format SOFA, modèles d'ombre sphérique de tête |
| **Synthèse & Modélisation Physique** | Réseaux de guides d'ondes numériques (DWM), modèle de cordes Karplus-Strong, filtres à variables d'état |
| **Conception de Filtres & Analyse Spectrale** | Rééchantillonneurs polyphases FIR/IIR, FFTW3 / pffft, transformée de Hilbert, rétroaction sans délai (ZDF) |
| **Frameworks de Plugins Audio** | API CLAP (Clever Audio Plugin), JUCE 8, SDK VST3, WebAudio AudioWorklet |
| **Systèmes et Plateformes Temps Réel** | Configuration Linux RT-PREEMPT, ALSA / JACK / PipeWire, plateforme Bela, Teensy 4.1 |

---

## 🚀 Projets Open-Source Majeurs

### 1. `reson-dsp` — Synthétiseur Polyphonique par Guides d'Ondes et Modélisation Physique
- **Langage** : C++23 / API CLAP
- **Description** : Moteur de synthèse polyphonique temps réel modélisant la résonance acoustique d'éléments métalliques percutés, de cloches et de cordes non linéaires via des réseaux bidimensionnels de guides d'ondes numériques.
- **Points Forts** :
  - Allocation de voix déterministe en $O(1)$ reposant sur des files circulaires sans verrou bornées à la compilation.
  - Zéro allocation dynamique de mémoire (zéro `malloc`) pendant toute la phase de traitement audio.
  - Cascades de filtres biquad vectorisées en AVX-512 et ARM NEON tournant à 192 kHz avec une empreinte CPU inférieure à 2.8% sur un seul cœur.

### 2. `spatial-orb` — Spatialisateur 3D Binaural Ambisonique Temps Réel
- **Langage** : Rust / WebAssembly
- **Description** : Moteur de spatialisation 3D décodant des flux Ambisoniques d'ordre élevé (jusqu'au 5e ordre HOA, 36 harmoniques sphériques) vers un rendu binaural au casque avec profils HRTF personnalisés.
- **Points Forts** :
  - Convolution rapide par blocs partitionnés (Overlap-Save) maintenant la latence sous le seuil de 1.2 ms.
  - Effet Doppler paramétrique continu et atténuation logarithmique de distance exempts de tout bruit de fermeture éclair (zipper noise).
  - Double cible de compilation : bibliothèques statiques natives (`.a` / `.so`) et WebAssembly pour intégration dans WebAudio AudioWorklet.

### 3. `wav-crunch` — Outil CLI d'Analyse Audio 64 bits et Rééchantillonneur Polyphase
- **Langage** : Rust
- **Description** : Utilitaire en ligne de commande haute précision, sans dépendances externes, dédié à l'analyse au niveau du bit, à la détection des crêtes réelles (True Peak par suréchantillonnage 4x) et à la conversion de fréquence d'échantillonnage de haute fidélité.
- **Points Forts** :
  - Interpolation sinc polyphase avec pondération dynamique offrant un rapport signal sur bruit (SNR) supérieur à 144 dB.
  - Traitement multitâche par vol de travail (work-stealing) aligné sur les lignes de cache processeur.
  - Exportation complète des métriques d'intensité sonore LUFS (norme ITU-R BS.1770-4), de plage dynamique et de matrices de corrélation de phase.

### 4. `patch-wire` — Moteur de Graphes de Signaux Audio Modulaire Léger
- **Langage** : C++20 / C
- **Description** : Moteur de calcul audio à graphe orienté acyclique (DAG) conçu pour les systèmes Linux embarqués (Raspberry Pi CM4, Bela) et les modules numériques Eurorack autonomes.
- **Points Forts** :
  - Tri topologique calculé une fois pour toutes lors de la configuration du graphe ; zéro saut conditionnel dans la boucle audio critique.
  - Empreinte mémoire statique bornée : l'ensemble des structures de données du graphe réside dans une arène contiguë alignée sur le cache.
  - Synchronisation temporelle stricte des signaux de contrôle analogique CV/Gate via les pilotes de bus SPI et I2C temps réel.

---

## 📊 Architecture du Pipeline Audio Temps Réel

```text
[ Pilote Matériel Audio (ALSA / ASIO / CoreAudio) ]
                        |
                        v (Interruption / Rappel Audio)
+-------------------------------------------------------------------+
|               Fonction de Rappel du Thread Audio Temps Réel       |
|                                                                   |
|   +-----------------------------------------------------------+   |
|   | 1. Dépilement FIFO SPSC Sans Verrou (Zéro Attente)        |   |
|   +-----------------------------------------------------------+   |
|                               |                                   |
|   +-----------------------------------------------------------+   |
|   | 2. Calcul Vectoriel SIMD par Blocs (Filtres DSP / DWM)    |   |
|   |    - Blocs de 64 échantillons                             |   |
|   |    - Registres vectoriels SoA (AVX-512 / NEON)            |   |
|   +-----------------------------------------------------------+   |
|                               |                                   |
|   +-----------------------------------------------------------+   |
|   | 3. Convolution Rapide Partitionnée HRTF Binaurale         |   |
|   |    - Tampons de recouvrement temporel (Overlap-Save)      |   |
|   +-----------------------------------------------------------+   |
|                               |                                   |
|   +-----------------------------------------------------------+   |
|   | 4. Limiteur de Saturation & Dithering vers Tampon DAC     |   |
|   +-----------------------------------------------------------+   |
+-------------------------------------------------------------------+
                        |
                        v
         [ Sortie DAC Matérielle / Casque ]
```

---

## ⏱️ Objectifs de Latence & Mesures Comparatives

Mesures relevées sous noyau Linux 6.11 avec correctif `PREEMPT_RT`, processeurs Intel Core i7-13700K (fréquence verrouillée à 4.8 GHz) et AMD Ryzen 9 7950X :

| Taille de Tampon | Fréquence d'Échantillonnage | Latence d'Aller-Retour Matérielle (I/O) | Temps d'Exécution Maximum Bloc DSP | Nombre de xruns (24h sous charge continue) |
| :---: | :---: | :---: | :---: | :---: |
| **32 échantillons** | 96 kHz | **0.67 ms** | 18.4 µs | **0** |
| **64 échantillons** | 96 kHz | **1.33 ms** | 34.2 µs | **0** |
| **128 échantillons** | 192 kHz | **1.33 ms** | 56.8 µs | **0** |
| **256 échantillons** | 48 kHz | **5.33 ms** | 41.1 µs | **0** |

---

## 🔬 Laboratoire d'Instrumentation & Studio Acoustique

| Catégorie | Équipements et Instruments |
| :--- | :--- |
| **Écoutes et Casques de Référence** | Enceintes de monitoring Neumann KH 120 II DSP, Sennheiser HD 800 S (profil d'égalisation en champ diffus), Beyerdynamic DT 1990 Pro |
| **Mesures Acoustiques & Capteurs** | Microphone de mesure étalonné Earthworks M30, réseaux de micros tétraédriques Ambisoniques d'ordre 1 et 2, logiciel REW |
| **Synthétiseurs Matériels & Systèmes Modulaires** | Système Eurorack 9U DIY sur mesure (oscillateurs analogiques VCO, multiplicateurs d'onde Serge, modules DSP Teensy maison) |
| **Appareils de Mesure Électronique** | Oscilloscope numérique 4 voies Rigol DS1054Z, analyseur logique Saleae Logic Pro 8, analyseur de signaux Audio Precision APx515 |
| **Bancs de Test Embarqués** | Kit de développement Bela Mini, Teensy 4.1 avec Audio Shield rev D, Raspberry Pi CM4 avec carte HiFiBerry DAC+ ADC Pro |

---

## 📬 Contact & Collaborations

- **GitHub Issues et Discussions** : Canal privilégié pour le signalement de bogues, les propositions d'évolution (RFC) et les discussions mathématiques en traitement du signal.
- **Empreinte PGP de Signature de Code** : `4A8F B120 79E3 5DC6 D982 314F 88B1 C990 2A3E 761F`
- **Résidence** : Séoul, République de Corée / Berlin, Allemagne (UTC+9 / UTC+1)
- **Préférence de Licences** : Utilitaires et algorithmes : Licence MIT / En-têtes bas niveau embarqués : ISC ou BSD-2-Clause
