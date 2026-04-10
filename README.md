# EEG Research Frontiers: From Basic Brain Science to AI (2024-2026)

> A comprehensive, progressive survey of electroencephalography research — from the biophysical foundations of neural signals to cutting-edge foundation models and brain-computer interfaces.

**Last updated**: 2026-04-10 | **Papers cited**: 70+ | **Datasets listed**: 15+

---

## Table of Contents

- [Part 0: The Brain — A Primer for Engineers](#part-0-the-brain)
  - [0.1 Brain Anatomy Essentials](#01-brain-anatomy-essentials)
  - [0.2 How Neurons Communicate](#02-how-neurons-communicate)
  - [0.3 From Neurons to Oscillations](#03-from-neurons-to-oscillations)
  - [0.4 The EEG Signal Chain](#04-the-eeg-signal-chain)
  - [0.5 EEG vs Other Neuroimaging](#05-eeg-vs-other-neuroimaging)
- [Part I: Foundations — What is EEG and Why Does It Matter?](#part-i-foundations)
  - [1.1 The Biophysics of Neural Signals](#11-the-biophysics-of-neural-signals)
  - [1.2 Neural Oscillations: The Brain's Frequency Bands](#12-neural-oscillations)
  - [1.3 EEG Recording: From Scalp to Signal](#13-eeg-recording)
  - [1.4 Event-Related Potentials (ERPs)](#14-event-related-potentials)
- [Part II: Classical Signal Processing](#part-ii-classical-signal-processing)
  - [2.1 Preprocessing Pipeline](#21-preprocessing-pipeline)
  - [2.2 Source Localization](#22-source-localization)
  - [2.3 Connectivity and Network Analysis](#23-connectivity-and-network-analysis)
- [Part III: Neuroscience Frontiers via EEG](#part-iii-neuroscience-frontiers)
  - [3.1 Consciousness and Awareness](#31-consciousness-and-awareness)
  - [3.2 Sleep and Memory Consolidation](#32-sleep-and-memory-consolidation)
  - [3.3 Attention and Cognitive Load](#33-attention-and-cognitive-load)
  - [3.4 New Theories of Neural Oscillations (2024-2026)](#34-new-theories-of-neural-oscillations)
- [Part IV: EEG + Deep Learning](#part-iv-eeg--deep-learning)
  - [4.1 EEG Foundation Models](#41-eeg-foundation-models)
  - [4.2 Self-Supervised and Transfer Learning](#42-self-supervised-and-transfer-learning)
  - [4.3 Brain Decoding: EEG-to-Text and Visual Reconstruction](#43-brain-decoding)
  - [4.4 EEG Signal Classification](#44-eeg-signal-classification)
- [Part V: Brain-Computer Interfaces](#part-v-brain-computer-interfaces)
  - [5.1 Motor Imagery BCI](#51-motor-imagery-bci)
  - [5.2 P300 and SSVEP](#52-p300-and-ssvep)
  - [5.3 Emerging BCI Paradigms](#53-emerging-bci-paradigms)
- [Part VI: Clinical Applications](#part-vi-clinical-applications)
  - [6.1 Epilepsy Detection and Prediction](#61-epilepsy)
  - [6.2 Sleep Staging](#62-sleep-staging)
  - [6.3 Neurodegenerative Disease Biomarkers](#63-neurodegenerative-disease)
  - [6.4 Psychiatric Disorders](#64-psychiatric-disorders)
  - [6.5 Brain Age Estimation](#65-brain-age)
- [Part VII: Datasets, Tools, and Infrastructure](#part-vii-infrastructure)
  - [7.1 Major Public Datasets](#71-datasets)
  - [7.2 Open Source Tools](#72-tools)
  - [7.3 EEG Foundation Model Repositories](#73-foundation-model-repos)
- [Part VIII: Research Community](#part-viii-community)
  - [8.1 Key Research Groups](#81-research-groups)
  - [8.2 Competitions and Challenges](#82-competitions)
  - [8.3 Conferences and Workshops](#83-conferences)
- [Part IX: Emerging Directions (2025-2027)](#part-ix-emerging-directions)

---

## Part 0: The Brain — A Primer for Engineers

> *You do not need a neuroscience degree to work with EEG data, but you do need a mental model of where the signal comes from. This section builds that model from first principles — anatomy, electrophysiology, circuit dynamics — so that everything in Parts I through IX rests on solid ground.*

### 0.1 Brain Anatomy Essentials

**The cerebral cortex** is the 2-4 mm thick, deeply folded sheet of neural tissue covering the brain. Its folds create **gyri** (ridges) and **sulci** (grooves), expanding the surface area to roughly 2,500 cm^2 — about the size of a large dinner napkin — packed into the skull. The cortex is divided into four lobes:

| Lobe | Location | Primary Functions |
|------|----------|-------------------|
| **Frontal** | Front of the brain | Motor control, planning, decision-making, working memory, speech production (Broca's area) |
| **Parietal** | Top-back | Somatosensory processing, spatial awareness, attention, sensorimotor integration |
| **Temporal** | Sides (near ears) | Auditory processing, language comprehension (Wernicke's area), memory formation |
| **Occipital** | Back | Visual processing — the dominant alpha rhythm originates here |

**Grey matter vs white matter.** The cortex (grey matter) contains the **cell bodies** of neurons, where computation happens. Beneath it, **white matter** consists of myelinated axon bundles — the brain's long-range "wiring." Think of grey matter as the compute nodes and white matter as the network cables. EEG overwhelmingly reflects grey matter activity, since that is where the current sources are.

**Cortical layers.** The cortex is organized into **six layers** (I-VI), each with distinct cell types and connectivity patterns. For EEG, **layer 5 (and layer 3) pyramidal neurons** are the stars. These cells have long apical dendrites that extend vertically from deep layers toward the cortical surface. When thousands of them receive synaptic input simultaneously, they produce open-field currents that sum constructively — forming the dipoles that EEG electrodes detect. Layer 5 pyramidal cells are the most excitable cortical neurons, generate the largest postsynaptic currents, and contribute roughly 80% of the extracellular signal strength (Reimann et al., *PLOS Computational Biology*, 2013; Teleniczky et al., *Nature Communications*, 2021).

**Subcortical structures relevant to EEG:**
- **Thalamus** — The brain's "relay station." Nearly all sensory information passes through the thalamus on its way to the cortex. Critically, the thalamus does not just relay: it participates in thalamo-cortical loops that generate alpha and delta rhythms. When you close your eyes and alpha power surges, that is the thalamus talking.
- **Hippocampus** — A seahorse-shaped structure deep in the temporal lobe, essential for forming new episodic memories. It generates a prominent theta rhythm (4-8 Hz) during memory encoding and spatial navigation. Hippocampal signals are too deep for scalp EEG to detect directly, but their influence on cortical activity is measurable.
- **Basal ganglia** — A set of nuclei involved in motor control, procedural learning, and reward. Dysfunction here underlies Parkinson's disease. Basal ganglia influence cortical beta oscillations (13-30 Hz) associated with motor planning and suppression.

**Cortical columns.** The cortex is organized into vertical **minicolumns** (~80-100 neurons, ~30-50 um diameter) and larger **macrocolumns** (~300-500 um diameter, containing 50-100 minicolumns). Within a column, neurons share common inputs and outputs and are densely interconnected vertically, while lateral connections are sparser (Mountcastle, *Brain*, 1997). For EEG, columns matter because synchronous activity within a macrocolumn is the minimal spatial unit that can produce a detectable signal, and neighboring columns tend to synchronize, producing the large-scale coherent dipoles that EEG measures.

**Scale.** The human brain contains approximately **86 billion neurons** connected by roughly **100 trillion (10^14) synapses** (Azevedo et al., *Journal of Comparative Neurology*, 2009). Of these, about 16 billion reside in the cortex. Each cortical neuron receives 5,000-10,000 synaptic inputs. The sheer scale means that EEG, even with 256 electrodes, is observing the aggregate behavior of millions of neurons per electrode — like hearing the roar of a stadium, not individual voices.

**Key references:**
- Kandel, Schwartz, Jessell, Siegelbaum & Hudspeth, *Principles of Neural Science* (McGraw-Hill, 6th ed., 2021) — The comprehensive neuroscience textbook.
- Azevedo et al., "Equal Numbers of Neuronal and Non-Neuronal Cells Make the Human Brain an Isometrically Scaled-Up Primate Brain" (*J. Comp. Neurol.*, 2009).
- Mountcastle, "The Columnar Organization of the Neocortex" (*Brain*, 1997).

### 0.2 How Neurons Communicate

**Action potentials.** A neuron at rest maintains a voltage of about -70 mV across its membrane (inside negative relative to outside). When excitatory input pushes this voltage past a threshold (~-55 mV), voltage-gated sodium channels open in a rapid cascade, depolarizing the membrane to about +30 mV within ~1 ms — the **action potential** (AP, or "spike"). This all-or-nothing signal propagates down the axon at 1-100 m/s (depending on myelination) to the synaptic terminals. The AP is like a digital "1" — it either fires or it does not, with no graded amplitude.

**Synaptic transmission.** When an AP arrives at a synapse, it triggers release of **neurotransmitter** molecules into the synaptic cleft (~20 nm gap). The two most important:
- **Glutamate** — The brain's primary excitatory neurotransmitter (~80% of cortical synapses). Binding to post-synaptic receptors (AMPA, NMDA) opens cation channels, depolarizing the post-synaptic neuron.
- **GABA** (gamma-aminobutyric acid) — The primary inhibitory neurotransmitter (~20% of cortical synapses). Opens chloride channels, hyperpolarizing the post-synaptic neuron.

The balance between glutamate (excitation, "E") and GABA (inhibition, "I") — the **E/I balance** — is a fundamental organizing principle. Disruptions in E/I balance are implicated in epilepsy (too much E), autism, schizophrenia, and many other conditions.

**Post-synaptic potentials (PSPs).** When neurotransmitters bind to post-synaptic receptors, they produce slow, graded voltage changes: **EPSPs** (excitatory, +0.5-1 mV) and **IPSPs** (inhibitory, -0.5-1 mV). Unlike the 1 ms action potential, a single PSP lasts **10-100 ms**. This temporal duration is critical for EEG.

**Why PSPs — not action potentials — dominate the EEG signal:**
1. **Duration**: A PSP lasts 10-100x longer than an AP. Longer-duration signals have a much higher probability of overlapping in time across thousands of neurons, enabling temporal summation.
2. **Spatial alignment**: Pyramidal cells in layers 3 and 5 are aligned perpendicular to the cortical surface, with apical dendrites pointing "up" (toward the scalp). Synaptic currents flowing along these aligned dendrites produce **open-field dipoles** that add constructively. Action potentials, by contrast, produce brief quadrupolar fields that cancel out rapidly with distance.
3. **Synchrony requirement**: EEG requires ~10,000-50,000 neurons to fire synchronously within a cortical patch of ~6 cm^2 to produce a measurable scalp signal. The long duration of PSPs makes this synchrony far more achievable than with 1 ms spikes.

**Neural populations.** A single neuron's contribution to scalp EEG is completely invisible — nanovolts at the scalp. EEG is fundamentally a **population-level measurement**: what you see reflects the synchronized post-synaptic activity of millions of pyramidal neurons. Think of a satellite photograph of city lights at night — you see the glow of neighborhoods, not individual bulbs. This is both the strength of EEG (large-scale brain dynamics) and its limitation (single-cell information is irrecoverably lost).

**Key references:**
- Bear, Connors & Paradiso, *Neuroscience: Exploring the Brain* (Wolters Kluwer, 4th ed., 2016) — Accessible introduction to neural signaling.
- Buzsaki, Anastassiou & Koch, "The Origin of Extracellular Fields and Currents" (*Nature Reviews Neuroscience*, 2012) — Definitive review of how cellular activity produces measurable electrical fields.
- Reimann et al., "A Biophysically Detailed Model of Neocortical Local Field Potentials" (*PLOS Computational Biology*, 2013).

### 0.3 From Neurons to Oscillations

Why does the brain oscillate at all? Oscillations are not an accident — they are a fundamental computational mechanism. Here is how they arise at different scales.

**Inhibitory interneuron networks create rhythmic pacing.** The basic mechanism is surprisingly simple. Fast-spiking, parvalbumin-expressing (PV+) interneurons form densely interconnected inhibitory networks. When one fires, it inhibits its neighbors. After the inhibition decays (~10-25 ms), those neighbors fire and inhibit their neighbors, producing a self-sustaining rhythm. The frequency is set by the time constant of the inhibitory post-synaptic potential: fast decay (~10 ms) yields **gamma oscillations** (30-100 Hz), while slower kinetics produce lower-frequency rhythms. This "interneuron network gamma" (ING) mechanism is one of the best-understood oscillatory generators in the brain (Bartos, Vida & Jonas, *Nature Reviews Neuroscience*, 2007).

**Thalamo-cortical loops: the "clock generator" for alpha and delta.** The thalamus and cortex form reciprocal loops: cortical layer 6 neurons project down to the thalamus, and thalamic relay neurons project up to cortical layer 4. Thalamic neurons possess unique ionic conductances (T-type calcium channels, h-current) that enable them to oscillate intrinsically between a "burst mode" (~0.5-4 Hz, generating delta during sleep) and a "tonic mode." The thalamo-cortical loop resonates at **~10 Hz**, producing the **alpha rhythm** — the most prominent oscillation in awake human EEG. When you close your eyes and visual cortex is freed from external input, the thalamo-cortical loop rings at its natural frequency, and alpha power increases dramatically (Lopes da Silva et al., 1974; Hughes & Crunelli, *Neuroscientist*, 2005).

**Local cortical circuits generate gamma oscillations.** Within the cortex, the interplay between excitatory pyramidal neurons and inhibitory interneurons (the "PING" model — Pyramidal-Interneuron Network Gamma) produces gamma-band activity. Pyramidal cells excite interneurons, which then inhibit the pyramidal cells, creating a cycle with a period of ~10-30 ms (30-100 Hz). Gamma oscillations are typically local (small cortical patches) and reflect active computation — feature binding in visual cortex, memory retrieval, conscious perception.

**Hippocampal theta: the memory rhythm.** The hippocampus generates a robust 4-8 Hz theta rhythm during memory encoding, spatial navigation, and REM sleep. Theta is driven by input from the medial septum (which paces hippocampal interneurons) and by intrinsic hippocampal circuitry. Theta provides a temporal scaffolding for memory: individual items are encoded within different gamma cycles nested within each theta cycle (the "theta-gamma code"), allowing the hippocampus to sequence multiple memories within a single oscillatory period (Lisman & Jensen, *Neuron*, 2013).

**Why does the brain oscillate? Functional theories:**
- **Communication through coherence (CTC)**: Two brain regions can communicate effectively only when their oscillatory cycles are aligned in phase. When a sending region's output arrives during the receiving region's excitable phase, the signal is amplified; otherwise it is suppressed. Oscillations thus act as a dynamic routing mechanism — the brain's equivalent of time-division multiplexing in telecommunications (Fries, *Neuron*, 2015).
- **Temporal binding**: Neurons representing different features of the same object (color, shape, motion) oscillate in synchrony (typically in the gamma band), "binding" them into a unified percept. This solves the computational problem of how distributed representations are integrated without a central processor.
- **Metabolic efficiency**: Oscillatory cycles create brief windows for spiking followed by longer inhibitory periods. This pulsed regime is more energy-efficient than continuous firing, reducing metabolic cost while maintaining information throughput — important for an organ consuming 20% of the body's energy at only 2% of its mass.

**Key references:**
- Buzsaki, *Rhythms of the Brain* (Oxford, 2006) — The foundational text on neural oscillations.
- Bartos, Vida & Jonas, "Synaptic Mechanisms of Synchronized Gamma Oscillations in Inhibitory Interneuron Networks" (*Nature Reviews Neuroscience*, 2007).
- Fries, "Rhythms for Cognition: Communication through Coherence" (*Neuron*, 2015).
- Lisman & Jensen, "The Theta-Gamma Neural Code" (*Neuron*, 2013).
- Hughes & Crunelli, "Thalamic Mechanisms of EEG Alpha Rhythms and Their Pathological Implications" (*Neuroscientist*, 2005).

### 0.4 The EEG Signal Chain

Follow a signal from its birth in the brain to its digital representation on your screen:

**Step 1: Pyramidal cell PSPs.** Thousands of layer 3/5 pyramidal neurons in a cortical patch receive synchronous synaptic input (e.g., from the thalamus during an alpha cycle). Their apical dendrites depolarize, creating a current sink near the synapse and a current source at the cell body — an **equivalent current dipole** with a magnitude of ~20 nA*m per neuron.

**Step 2: Local field potential (LFP).** The superposition of dipoles from ~10,000+ synchronous neurons produces a measurable **local field potential** in the surrounding tissue. The LFP is the signal measured by intracranial electrodes and represents activity within ~1-3 mm of the electrode tip.

**Step 3: Volume conduction through tissue.** The dipole's electric field propagates outward through brain tissue, cerebrospinal fluid (CSF), skull, and scalp. Each layer has different conductivity: brain (~0.33 S/m), CSF (~1.79 S/m), skull (~0.01 S/m — the major resistive barrier), and scalp (~0.43 S/m). The skull attenuates and smears the signal dramatically, acting as a low-pass spatial filter.

**Step 4: Scalp potential.** By the time the signal reaches the scalp, it is 10-100 uV — roughly 1,000x weaker than the LFP. A cortical dipole at depth *d* produces a scalp projection with spatial extent ~2*d*, limiting spatial resolution to 1-2 cm at best.

**Step 5: Electrode and amplifier.** The Ag/AgCl electrode transduces the ionic scalp current into electronic current. A differential amplifier measures the voltage between the electrode and a reference, rejecting common-mode noise. Modern amplifiers have input impedance >100 MOhm, common-mode rejection ratio >80 dB, and noise floor <1 uV.

**Step 6: Digital signal.** An ADC samples the amplified signal at 250-2048 Hz with 16-24 bit resolution, producing the discrete time series you analyze.

**What is lost at each step:**
- **Spatial resolution**: Volume conduction through the skull smears each cortical source across 5-10 cm of scalp. Two sources 2 cm apart may be indistinguishable.
- **Deep sources**: Subcortical structures (hippocampus, basal ganglia, thalamus) are too deep for their fields to propagate to the scalp at measurable amplitudes. EEG is fundamentally a cortical surface measurement.
- **High frequencies**: The skull and scalp act as a low-pass spatial filter. Gamma activity (>30 Hz) is attenuated more severely than lower frequencies, which is why gamma research often requires intracranial recordings.
- **Radial vs tangential sources**: Sources in **sulci** (oriented tangentially to the scalp) produce fields that partially cancel due to opposing dipoles on opposite walls. Sources on **gyral crowns** (oriented radially) produce strong, detectable signals. This means roughly one-third of the cortical surface — the sulcal walls — is effectively invisible to EEG.

**The forward problem** (from sources to scalp) can be solved exactly given a head model and known source configuration. Boundary Element Method (BEM) and Finite Element Method (FEM) are standard numerical approaches. The solution is unique — a given source configuration produces exactly one scalp distribution.

**The inverse problem** (from scalp to sources) is **fundamentally ill-posed**: infinitely many source configurations can produce the same scalp distribution. This is not a practical limitation that better math will solve — it is a mathematical fact (Helmholtz, 1853). All source localization methods (dipole fitting, beamforming, eLORETA) make additional assumptions (minimum norm, smoothness, sparsity) to select one solution from the infinite set. This is why source localization results should always be interpreted with caution.

**Key references:**
- Nunez & Srinivasan, *Electric Fields of the Brain* (Oxford, 2006) — Chapters 1-4 cover the full signal chain.
- Hallez et al., "Review on Solving the Forward Problem in EEG Source Analysis" (*J. NeuroEngineering and Rehabilitation*, 2007).
- Grech et al., "Review on Solving the Inverse Problem in EEG Source Analysis" (*J. NeuroEngineering and Rehabilitation*, 2008).

### 0.5 EEG vs Other Neuroimaging

| Method | What It Measures | Spatial Resolution | Temporal Resolution | Invasiveness | Approximate Cost | Portability |
|--------|-----------------|-------------------|---------------------|-------------|-----------------|-------------|
| **EEG** | Post-synaptic potentials (scalp voltage) | ~1-2 cm | **~1 ms** | Non-invasive | $10K-100K | **High** (wearable systems exist) |
| **MEG** | Magnetic fields from PSPs | ~3-5 mm | **~1 ms** | Non-invasive | $2-3M | None (requires shielded room) |
| **fMRI** | Blood oxygenation (BOLD signal, a proxy for neural activity) | **~1-2 mm** | ~1-2 s | Non-invasive | $1-3M | None (requires MRI scanner) |
| **fNIRS** | Blood oxygenation (near-infrared absorption) | ~1-3 cm | ~100 ms | Non-invasive | $20K-100K | **High** (wearable) |
| **ECoG** | Cortical surface field potentials | **~1 mm** | **~1 ms** | **Invasive** (surgical) | N/A (clinical) | None |
| **Single-unit** | Individual neuron action potentials | **~single neuron** | **~0.1 ms** | **Invasive** (penetrating electrodes) | N/A (clinical/research) | None |
| **PET** | Metabolic activity (radiotracer uptake) | ~4-8 mm | ~30-60 s | Invasive (injection) | $2-5M | None |

**When to use what:**
- **EEG** excels when you need millisecond timing (e.g., studying when a cognitive process occurs), low cost, portability, or long-duration recordings (e.g., sleep studies, BCI). Its weakness is spatial ambiguity.
- **MEG** offers similar temporal resolution with better spatial resolution (magnetic fields are not smeared by the skull), but requires expensive magnetically-shielded rooms and SQUID sensors.
- **fMRI** is the gold standard for *where* in the brain something happens (millimeter precision), but its temporal resolution is limited by the hemodynamic response (~5-6 s delay). It cannot tell you *when* a process unfolds at the sub-second level.
- **fNIRS** is the portable, affordable alternative to fMRI. It measures the same hemodynamic signal but with lower spatial resolution. Increasingly used in naturalistic settings (classrooms, social interactions).
- **ECoG** (electrocorticography) combines the best of both worlds — millimeter spatial resolution with millisecond temporal resolution — but requires a craniotomy. Used clinically for pre-surgical epilepsy mapping and in cutting-edge BCI research (e.g., the Stanford BrainGate and UCSF speech decoding projects).
- **Single-unit recording** is the ultimate resolution: individual neuron spike trains. Essential for understanding neural coding but limited to small brain regions in animal research or rare clinical settings.
- **PET** provides unique information about neurotransmitter systems and metabolic activity but involves radioactive tracers and poor temporal resolution.

**The complementarity principle**: No single method captures the full picture. The field increasingly combines modalities — simultaneous EEG-fMRI, EEG-fNIRS for portable multimodal recordings, and ECoG-informed EEG source modeling for ground-truth validation.

**Key references:**
- Baillet, "Magnetoencephalography for Brain Electrophysiology and Imaging" (*Nature Neuroscience*, 2017).
- Logothetis, "What We Can Do and What We Cannot Do with fMRI" (*Nature*, 2008).
- Pinti et al., "The Present and Future Use of Functional Near-Infrared Spectroscopy (fNIRS) for Cognitive Neuroscience" (*Annals of the New York Academy of Sciences*, 2020).
- Hill et al., "Recording Human Electrocorticographic (ECoG) Signals for Neuroscientific Research and Real-Time Functional Cortical Mapping" (*J. Visualized Experiments*, 2012).

---

## Part I: Foundations

### 1.1 The Biophysics of Neural Signals

EEG measures **voltage fluctuations** on the scalp produced by the **synchronous activity of large populations of cortical pyramidal neurons**. Key principles:

- **What EEG actually measures**: Post-synaptic potentials (PSPs) of cortical pyramidal cells oriented perpendicular to the cortical surface. Action potentials are too brief and asynchronous to summate at the scalp.
- **Why synchrony matters**: A single neuron's PSP is ~20-40 µV at the soma. Scalp EEG records ~10-100 µV, requiring ~10,000-50,000 neurons firing synchronously within a cortical patch of ~6 cm² (Nunez & Srinivasan, 2006).
- **Volume conduction**: Signals propagate through CSF, skull, and scalp, causing spatial smearing. A dipole source at depth d has scalp projection width ~2d. This limits spatial resolution to ~1-2 cm.
- **Temporal resolution advantage**: EEG captures neural dynamics at **millisecond resolution** — orders of magnitude faster than fMRI (~1-2 seconds). This makes EEG uniquely suited for studying rapid cognitive processes.

**Key references**:
- Nunez & Srinivasan, *Electric Fields of the Brain* (Oxford, 2006) — The definitive textbook on EEG biophysics.
- Lopes da Silva, "EEG and MEG: Relevance to Neuroscience" (*Neuron*, 2013) — Review of what EEG can and cannot tell us about brain function.
- Buzsáki, Anastassiou & Koch, "The Origin of Extracellular Fields and Currents" (*Nature Reviews Neuroscience*, 2012) — How different cell types contribute to extracellular signals.

### 1.2 Neural Oscillations

The brain produces rhythmic activity at characteristic frequency bands, each associated with different cognitive states:

| Band | Frequency | Typical Amplitude | Associated States | Key Brain Regions |
|------|-----------|------------------|-------------------|-------------------|
| **Delta** (δ) | 0.5-4 Hz | 20-200 µV | Deep sleep (N3), traumatic brain injury | Thalamus → cortex |
| **Theta** (θ) | 4-8 Hz | 5-100 µV | Memory encoding, navigation, drowsiness | Hippocampus, frontal midline |
| **Alpha** (α) | 8-13 Hz | 10-50 µV | Relaxed wakefulness, eyes closed, inhibition | Occipital (visual alpha), sensorimotor (mu rhythm) |
| **Beta** (β) | 13-30 Hz | 5-30 µV | Active thinking, motor planning, anxiety | Motor cortex, frontal |
| **Gamma** (γ) | 30-100+ Hz | 1-10 µV | Conscious perception, feature binding, memory recall | Widespread cortical |

**Key references**:
- Buzsáki, *Rhythms of the Brain* (Oxford, 2006) — The most influential book on neural oscillations.
- Jensen & Mazaheri, "Shaping Functional Architecture by Oscillatory Alpha Activity" (*Frontiers in Human Neuroscience*, 2010) — Alpha as an inhibitory mechanism.
- Fries, "Rhythms for Cognition: Communication through Coherence" (*Neuron*, 2015) — How oscillation-based synchrony enables information routing between brain areas.

### 1.3 EEG Recording

**Standard systems**:
- **10-20 system** (19-21 channels): Clinical standard. Electrode positions defined relative to skull landmarks (nasion, inion, preauricular points).
- **10-10 system** (64-128 channels): Research standard. Higher spatial resolution.
- **High-density EEG** (256-512 channels): Enables better source localization. Pioneered at UCSD SCCN.

**Signal characteristics**:
- Amplitude: 10-100 µV (vs. ECG ~1 mV, EMG ~10 mV)
- Sampling rate: typically 250-1000 Hz (up to 20 kHz for high-frequency oscillations)
- Impedance: <5 kΩ (wet electrodes), <50 kΩ (dry electrodes), <1 MΩ (capacitive)

**The electrode-skin interface** is the critical bottleneck: conductive gel reduces impedance but is time-consuming to apply. Dry and semi-dry electrodes (2023-2026) are an active area of development for consumer-grade and mobile EEG.

### 1.4 Event-Related Potentials

ERPs are time-locked voltage deflections extracted by averaging across many trials of the same stimulus:

| Component | Latency | Polarity | Cognitive Process | Classic Paradigm |
|-----------|---------|----------|-------------------|------------------|
| **N1/P1** | 80-120 ms | N/P | Early sensory processing | Any stimulus |
| **MMN** (Mismatch Negativity) | 100-250 ms | N | Pre-attentive change detection | Oddball (passive) |
| **N170** | 170 ms | N | Face processing | Face vs. object |
| **P300** (P3b) | 300-600 ms | P | Stimulus evaluation, context updating | Oddball (active) |
| **N400** | 400 ms | N | Semantic processing | Sentence reading |
| **P600** | 600 ms | P | Syntactic reanalysis | Garden-path sentences |
| **ERN** | 50-100 ms post-error | N | Error detection | Flanker/Stroop tasks |

**Key references**:
- Luck, *An Introduction to the Event-Related Potential Technique* (MIT Press, 2nd ed., 2014) — The standard textbook.
- Kappenman & Luck, *The Oxford Handbook of Event-Related Potential Components* (Oxford, 2011).

---

## Part II: Classical Signal Processing

### 2.1 Preprocessing Pipeline

Standard EEG preprocessing (in order):
1. **High-pass filter** (0.1-1 Hz) → remove slow drifts
2. **Line noise removal** (50/60 Hz notch or adaptive filter)
3. **Bad channel detection** → interpolation (spherical spline)
4. **Re-referencing** (average, linked mastoids, or REST)
5. **ICA** (Independent Component Analysis) → artifact removal (eye blinks, muscle, cardiac)
6. **Epoching** → segment around events
7. **Baseline correction** → subtract pre-stimulus mean
8. **Artifact rejection** → remove bad epochs (amplitude threshold or probability-based)

**Frontier (2024-2026): Deep learning for artifact removal**:
- ICLabel ([Pion-Tonachini et al., *NeuroImage*, 2019](https://github.com/sccn/ICLabel)) — Automated ICA component classification using a CNN. Integrated into EEGLAB and MNE.
- **IC-U-Net** (Cai et al., *NeuroImage*, 2024) — U-Net architecture for artifact removal directly in the time domain, without ICA.
- **EEGDfus** (2025) — Diffusion model for EEG denoising, generating clean EEG from corrupted signals.

### 2.2 Source Localization

The **inverse problem**: estimating brain source locations from scalp voltages. Key approaches:
- **Dipole fitting**: Assume 1-3 equivalent current dipoles. Fast but requires strong assumptions.
- **Beamforming** (LCMV, DICS): Spatial filtering. Good temporal resolution.
- **Distributed source models** (eLORETA, sLORETA, MNE): Estimate current density across cortex. No dipole count assumption.

**Frontier**: Deep learning source localization (Hecker et al., *NeuroImage*, 2024) — CNN-based inverse solutions trained on forward models.

### 2.3 Connectivity and Network Analysis

**Functional connectivity** methods:
- **Coherence**: Frequency-domain correlation. Simple but affected by volume conduction.
- **Phase-Locking Value (PLV)**: Phase synchrony independent of amplitude. Less affected by volume conduction.
- **Granger Causality / Transfer Entropy**: Directed connectivity. Captures causal influence.
- **Microstate analysis**: Segments EEG into quasi-stable topographic maps (typically 4-7 canonical states). Microstates correlate with fMRI resting-state networks.

**Frontier (2024-2026)**:
- **Graph neural networks for EEG connectivity** — Treating electrodes as graph nodes and learning dynamic adjacency matrices (Zhong et al., *IEEE TNNLS*, 2024).
- **Deep learning for brain connectivity** (Phang et al., NeurIPS 2025 workshop) — Learning connectivity patterns directly from raw EEG without explicit feature engineering.

---

## Part III: Neuroscience Frontiers via EEG

### 3.1 Consciousness and Awareness

EEG-based consciousness research is one of the most active frontiers:

- **Perturbational Complexity Index (PCI)** (Casali et al., *Science Translational Medicine*, 2013): TMS-EEG based measure. PCI reliably distinguishes conscious from unconscious states (97% accuracy across 200+ patients). Updated versions: PCI^st (2019), automated PCI (2024).
- **Spectral exponent (1/f slope)** as consciousness biomarker — Becker et al. (*NeuroImage*, 2025) showed the spectral exponent of EEG tracks consciousness levels across anesthesia, sleep, and disorders of consciousness. Steeper slope = less conscious.
- **Integrated Information Theory (IIT) + EEG**: Measuring Φ (integrated information) from EEG remains computationally challenging, but approximations using state-space models are advancing (Esteban et al., 2025).
- **Global Neuronal Workspace Theory (GNWT)**: P300 as the marker of conscious access. The "ignition" pattern (late widespread activation) is measured via EEG. Adversarial collaboration between IIT and GNWT ongoing (Melloni et al., *Nature Neuroscience*, 2024).

### 3.2 Sleep and Memory Consolidation

- **Sleep spindles and memory**: Sigma-band (12-15 Hz) spindles during N2 sleep are now linked to specific memory traces. Theta-tagged memories are preferentially replayed during spindles (Petzka et al., *Nature Neuroscience*, 2024).
- **Slow oscillation-spindle coupling**: The phase of slow oscillations (<1 Hz) modulates spindle timing, creating optimal windows for hippocampal-cortical memory transfer. Precise coupling strength predicts next-day memory performance (Helfrich et al., 2018; updated analyses 2024-2025).
- **Targeted Memory Reactivation (TMR)**: Presenting learning-associated cues (sounds, odors) during sleep enhances consolidation. EEG-triggered TMR (delivering cues at specific slow-oscillation phases) is an active intervention area.

### 3.3 Attention and Cognitive Load

- **Alpha desynchronization**: The classic marker. Attended stimuli cause alpha power decrease in relevant cortical areas. The "spotlight" metaphor: alpha suppresses irrelevant regions.
- **Frontal theta**: Increases with cognitive load (mental arithmetic, working memory). Used in neuroergonomics for real-time workload monitoring.
- **Neural markers of distraction**: The "attentional blink" (AB) and its EEG correlates (reduced P3 for missed targets) remain active research.

### 3.4 New Theories of Neural Oscillations (2024-2026)

- **pACF (periodic auto-correlation function)** — O'Byrne & Bhatt (*Nature Methods*, 2025): A new method for measuring neural oscillations that avoids confounds of traditional spectral analysis. pACF separates periodic from aperiodic components more cleanly than FOOOF/specparam.
- **Traveling waves in cortex**: EEG/ECoG evidence that oscillations are not standing waves but travel across cortex in organized patterns. Direction and speed of traveling waves correlate with cognitive state (Muller et al., 2018; updated analyses 2024).
- **Cross-frequency coupling**: Phase-amplitude coupling (PAC) between theta phase and gamma amplitude is a proposed mechanism for multi-item working memory. Each gamma burst within a theta cycle represents one memory item (Lisman & Jensen, 2013; ongoing validation).

---

## Part IV: EEG + Deep Learning

### 4.1 EEG Foundation Models

The biggest shift in EEG research (2023-2026): pre-training large models on massive EEG corpora, then fine-tuning for specific tasks.

| Model | Year | Venue | Pre-training Data | Params | Key Innovation | Code |
|-------|------|-------|-------------------|--------|----------------|------|
| **LaBraM** | 2024 | ICLR (Spotlight) | ~2,500 hrs from ~20 datasets | — | Masked neural code prediction with vector-quantized tokenizer | [GitHub](https://github.com/935963004/LaBraM) |
| **NeuroLM** | 2025 | ICLR | Multi-modal (EEG + text) | 1.7B | First billion-parameter EEG-language model; aligns neural and linguistic representations | [GitHub](https://github.com/935963004/NeuroLM) |
| **CBraMod** | 2025 | ICLR | EEG + multiple biosignals | — | Criss-cross brain foundation model; handles heterogeneous channel configs | [GitHub](https://github.com/wjq-learning/CBraMod) |
| **Brant-2** | 2024 | arXiv | 22K hours of clinical EEG | — | Largest single-source pre-training for EEG; supports 4 to 1024 channels | [arXiv](https://arxiv.org/abs/2402.10251) |
| **EEGPT** | 2024 | NeurIPS | Multiple EEG datasets | 10M | Mask-based dual self-supervised learning; spatio-temporal alignment | [GitHub](https://github.com/BINE022/EEGPT) |
| **REVE** | 2025 | arXiv | 25K subjects | — | Largest subject count for EEG pre-training | [Project](https://brain-bzh.github.io/reve/) |
| **FoME** | 2025 | — | Multi-institutional | — | EEG foundation model with clinical focus | — |
| **BENDR** | 2021 | arXiv | TUH corpus | — | Contrastive self-supervised learning; "thinker-invariant" representations | [GitHub](https://github.com/SPOClab-ca/BENDR) |
| **BIOT** | 2023 | NeurIPS | Multiple biosignals | — | Framework for biosignal pre-training at scale | [GitHub](https://github.com/ycq091044/BIOT) |
| **EEGMamba** | 2025 | Neural Networks | — | — | State-space model (Mamba) adapted for EEG | [GitHub](https://github.com/wjq-learning/EEGMamba) |

**Survey papers**:
- Eldele et al., "Self-Supervised Learning for EEG-Based Brain-Computer Interfaces: A Comprehensive Survey" (*ACM Computing Surveys*, 2025) — [DOI](https://dl.acm.org/doi/10.1145/3736574)
- Yang et al., "EEG Foundation Models: A Systematic Review" (arXiv, 2025) — [arXiv](https://arxiv.org/abs/2507.11783)
- Zhang et al., "LLMs for EEG: A Comprehensive Survey" (arXiv, 2025) — [arXiv](https://arxiv.org/abs/2506.06353)

### 4.2 Self-Supervised and Transfer Learning

Core challenge: EEG varies dramatically across subjects (anatomy, electrode placement, impedance). Pre-training addresses this via:

- **Contrastive learning**: Learn representations where same-subject/same-state EEG is close, different subjects far. BENDR, ContraWR (2023).
- **Masked signal prediction**: Mask portions of EEG, predict from context. LaBraM, CBraMod.
- **Domain adaptation**: Align source and target subject distributions. Key for practical BCI (no calibration needed).

**Benchmark**: EEG-FM-Bench (2025) — Unified evaluation of 7 foundation models across 14 datasets and 10 paradigms. Includes gradient analysis and representation probing. [GitHub](https://github.com/xw1216/EEG-FM-Bench)

### 4.3 Brain Decoding

#### EEG-to-Text
- **DeWave** (Duan et al., NeurIPS 2023) — Discrete codex for translating raw EEG into text. First large-scale attempt. [arXiv](https://arxiv.org/abs/2309.14030)
- **"Are EEG-to-Text Models Working?"** (Ameen & Leong, ACL 2024) — Critical evaluation showing many EEG-to-text results don't hold under proper controls. Essential reading. [Paper](https://aclanthology.org/2024.acl-long.727/)
- **NeuSpeech** (Yang et al., 2024) — Decoding continuous speech from non-invasive EEG using CTC alignment. [arXiv](https://arxiv.org/abs/2403.01748)

#### Visual Reconstruction from EEG
- **DreamDiffusion** (Bai et al., ECCV 2024) — Generating images from EEG signals using Stable Diffusion, with temporal masked signal modeling for EEG pre-training. [arXiv](https://arxiv.org/abs/2306.16934)
- **EEG2Video** (NeurIPS 2024) — Reconstructing video sequences from EEG with temporal coherence. [NeurIPS](https://neurips.cc/virtual/2024/poster/95156)
- **Perceptogram** (NeurIPS 2024) — Assessing visual perception capacity from EEG using deep generative models. [OpenReview](https://openreview.net/forum?id=RxkcroC8qP)

#### Inner/Imagined Speech
- **Imagined Speech from EEG** (Cho et al., *Cell*, 2025) — Decoded imagined sentences from high-density EEG using a contrastive language-brain model. Significant advance in non-invasive speech BCI.
- **Chisco dataset** (2024) — Largest per-individual imagined speech EEG dataset: >20,000 sentences, >900 minutes per subject. [Nature Scientific Data](https://www.nature.com/articles/s41597-024-04114-1)

### 4.4 EEG Signal Classification

**Emotion Recognition**:
- Leading datasets: DEAP (32 subjects), SEED (15 subjects, 3-7 emotion classes)
- State-of-the-art: Graph neural networks capturing spatial relationships between electrodes; cross-subject accuracy improving via domain adaptation (70-85% on SEED).

**Motor Imagery Classification**:
- EEGNet (Lawhern et al., 2018) — Compact CNN, still a strong baseline.
- Transformer-based: EEG Conformer (Song et al., 2023), ATCNet (Altaheri et al., 2023).
- State-of-the-art: ~85-90% on BCI Competition IV-2a (4-class).

---

## Part V: Brain-Computer Interfaces

### 5.1 Motor Imagery BCI

Motor imagery (imagining hand/foot movements) produces detectable event-related desynchronization (ERD) in mu (8-12 Hz) and beta (18-26 Hz) bands over sensorimotor cortex.

- **Deep learning for MI-BCI**: Transformers and attention mechanisms now dominate, replacing CSP+LDA pipelines. Min et al. (2024) achieved cross-subject MI decoding without calibration using pre-trained EEG models.
- **Transfer learning**: A key frontier — making BCIs work on new users without lengthy calibration. Domain adaptation methods (adversarial, optimal transport) show promise.

### 5.2 P300 and SSVEP

- **P300 Spellers**: User focuses on target letter in a grid; oddball P300 response identifies the target. Modern deep learning approaches (SpellerSSL, 2025) use self-supervised pre-training for P300 detection.
- **SSVEP (Steady-State Visual Evoked Potentials)**: Stare at flickering stimuli at different frequencies; frequency-tagged response identifies target. Tsinghua BCI Lab achieved **60+ characters/min** — fastest non-invasive BCI. Filter-bank CCA (FBCCA) remains the dominant signal processing approach.

### 5.3 Emerging BCI Paradigms

- **Hybrid BCIs**: Combining MI + SSVEP or MI + P300 for higher information transfer rates.
- **Error-related potentials (ErrP)**: Detecting when the BCI makes an error, enabling automatic correction.
- **Passive BCIs**: Monitoring cognitive state (fatigue, attention, workload) without explicit user commands. Applications in driving, aviation, education.

---

## Part VI: Clinical Applications

### 6.1 Epilepsy

- **Seizure detection**: Deep learning on continuous EEG achieves >95% sensitivity. Key dataset: CHB-MIT (PhysioNet). Recent: single-channel approaches for wearable devices.
- **Seizure prediction**: Predicting seizures 30-60 minutes in advance. Signal: pre-ictal changes in synchronization, entropy. Still challenging (many false positives). Self-supervised approaches (2024-2025) show improved patient-specific prediction.
- **High-Frequency Oscillations (HFOs)**: 80-500 Hz signals as biomarkers for epileptogenic zones. Automated HFO detection using deep learning (Gotman Lab, McGill).

### 6.2 Sleep Staging

Automatic classification of sleep into Wake, N1, N2, N3, REM using single or few EEG channels:
- **KAN-SleepNet** (2025) — Uses Kolmogorov-Arnold Networks for sleep staging.
- **MPSleepNet** (2025) — Multi-resolution preprocessing for improved staging accuracy.
- Standard benchmark: Sleep-EDF Expanded (PhysioNet). State-of-the-art: ~85-88% overall accuracy, ~90%+ for well-represented stages (N2, N3).

### 6.3 Neurodegenerative Disease

- **Alzheimer's**: EEG slowing (reduced alpha, increased theta/delta) is an early biomarker. STEADYNet (2025) — Spectral-temporal deep learning for AD detection. Alpha rhythm disruption detectable years before clinical diagnosis.
- **Parkinson's**: Beta-band abnormalities in basal ganglia-cortical circuits. Used for DBS (deep brain stimulation) tuning.
- **Brain age**: Models trained to predict chronological age from EEG. "Brain age gap" (predicted - actual) is a biomarker: positive gap indicates accelerated brain aging. Large-scale studies (7,000+ individuals, 2024) validate this approach.

### 6.4 Psychiatric Disorders

- **Depression**: Frontal alpha asymmetry (higher left alpha = more depression). Deep learning classification achieves ~80-85% accuracy. Loudness Dependence of Auditory Evoked Potentials (LDAEP) as serotonin biomarker.
- **ADHD**: Theta/Beta ratio elevated in ADHD (controversial — meta-analyses show effect is smaller than originally claimed). Machine learning for ADHD subtyping.
- **Schizophrenia**: Reduced P300 amplitude, gamma-band abnormalities, mismatch negativity deficits.

### 6.5 Brain Age

- **Brain age prediction from EEG** (Engemann et al., *eLife*, 2022; updated 2024) — Trained on 7,000+ individuals. Features: spectral power, connectivity, complexity measures. Brain age gap correlates with mortality, cognitive decline, and disease risk.

---

## Part VII: Infrastructure

### 7.1 Major Public Datasets

| Dataset | Year | Subjects | Channels | Task | Size | URL |
|---------|------|----------|----------|------|------|-----|
| **TUH EEG Corpus** | 2016+ | 10,874 | 19-24 | Clinical (normal/abnormal) | ~572 GB | [isip.piconepress.com](https://isip.piconepress.com/projects/tuh_eeg/) |
| **HBN-EEG** | 2023+ | 3,000+ | 128 | 6 cognitive tasks (ages 5-21) | Multi-TB | [neuromechanist.github.io](https://neuromechanist.github.io/data/hbn/) |
| **SEED / SEED-IV / SEED-VII** | 2015+ | 15 | 62 | Emotion (3/4/7 classes) | ~2 GB/ver | [bcmi.sjtu.edu.cn](https://bcmi.sjtu.edu.cn/home/seed/) |
| **DEAP** | 2012 | 32 | 32+8 periph | Emotion (valence, arousal) | ~3 GB | [eecs.qmul.ac.uk](http://eecs.qmul.ac.uk/mmv/datasets/deap/) |
| **BCI Competition IV-2a** | 2008 | 9 | 22 | 4-class motor imagery | — | [bbci.de](https://www.bbci.de/competition/iv/) |
| **CHB-MIT** | 2010 | 22 (pediatric) | 23 | Seizure detection | ~40 GB | [physionet.org](https://physionet.org/content/chbmit/1.0.0/) |
| **Sleep-EDF Expanded** | 2018 | 78 (197 rec) | 2+EOG+EMG | Sleep staging | — | [physionet.org](https://physionet.org/content/sleep-edfx/1.0.0/) |
| **EEG Motor Movement** | 2004 | 109 | 64 | Motor execution/imagery | ~3 GB | [physionet.org](https://physionet.org/content/eegmmidb/1.0.0/) |
| **THINGS-EEG** | 2022+ | 10-50 | 63-64 | Visual object recognition | ~100 GB+ | [osf.io](https://osf.io/3jk45/) |
| **Inner Speech** | 2022 | 10 | 128 | Inner/pronounced/visualized speech | 5,640 trials | [Nature](https://www.nature.com/articles/s41597-022-01147-2) |
| **Chisco** | 2024 | Multiple | HD-EEG | Imagined speech (20K+ sentences) | Largest/subject | [Nature](https://www.nature.com/articles/s41597-024-04114-1) |

### 7.2 Open Source Tools

| Tool | Language | Stars | Latest Ver | Key Features | URL |
|------|----------|-------|-----------|--------------|-----|
| **MNE-Python** | Python | ~3,200 | v1.11.0 | Full EEG/MEG pipeline, source localization, statistics | [github.com/mne-tools/mne-python](https://github.com/mne-tools/mne-python) |
| **EEGLAB** | MATLAB | ~754 | 2025.1.0 | ICA, DIPFIT, 100+ plugins, BIDS | [github.com/sccn/eeglab](https://github.com/sccn/eeglab) |
| **Braindecode** | PyTorch | ~1,200 | v1.4.0 | 30+ DL models, MNE integration | [github.com/braindecode/braindecode](https://github.com/braindecode/braindecode) |
| **TorchEEG** | PyTorch | ~558 | v1.1.3 | CNNs/GNNs/Transformers for EEG | [github.com/torcheeg/torcheeg](https://github.com/torcheeg/torcheeg) |
| **MOABB** | Python | ~966 | v1.5 | BCI benchmarking across 30+ datasets | [github.com/NeuroTechX/moabb](https://github.com/NeuroTechX/moabb) |

### 7.3 Foundation Model Repositories

| Model | Stars | URL |
|-------|-------|-----|
| LaBraM | ~590 | [github.com/935963004/LaBraM](https://github.com/935963004/LaBraM) |
| EEGPT | ~280 | [github.com/BINE022/EEGPT](https://github.com/BINE022/EEGPT) |
| BENDR | ~201 | [github.com/SPOClab-ca/BENDR](https://github.com/SPOClab-ca/BENDR) |
| BIOT | ~185 | [github.com/ycq091044/BIOT](https://github.com/ycq091044/BIOT) |
| EEG-FM-Bench | — | [github.com/xw1216/EEG-FM-Bench](https://github.com/xw1216/EEG-FM-Bench) |
| EEG Foundation Models Collection | — | [github.com/gayalkuruppu/eeg-foundation-models](https://github.com/gayalkuruppu/eeg-foundation-models) |

---

## Part VIII: Research Community

### 8.1 Key Research Groups

| Lab | Institution | PI | Focus |
|-----|-----------|-----|-------|
| Tsinghua BCI Lab | Tsinghua University | Xiaorong Gao | SSVEP-BCI (world-record speed), BETA benchmark |
| SCCN (Swartz Center) | UC San Diego | Scott Makeig | EEGLAB, Mobile Brain/Body Imaging, ICA |
| Graz BCI Lab | TU Graz, Austria | Gernot Muller-Putz | Motor imagery BCI pioneer |
| Gotman Lab | McGill University | Jean Gotman | Epilepsy EEG, HFO detection |
| BCMI Lab | SJTU, Shanghai | Bao-Liang Lu | SEED datasets, emotion recognition |
| INRIA MIND/TAU | INRIA, France | A. Gramfort et al. | MNE-Python, Braindecode, source localization |
| NeuroTechX | International | Community | MOABB, open-source neurotech |
| Sajda Lab | Columbia University | Paul Sajda | Neural engineering, EEG-based cognitive monitoring |
| He Lab | Carnegie Mellon | Bin He | Non-invasive BCI, source imaging |

### 8.2 Competitions and Challenges

| Competition | Year | Tasks | Scale | URL |
|------------|------|-------|-------|-----|
| **NeurIPS 2025 EEG Challenge** | 2025 | Zero-shot cross-task decoding + psychopathology prediction | 3,000+ subjects, 128-ch | [eeg2025.github.io](https://eeg2025.github.io/data/) |
| **HMS Harmful Brain Activity (Kaggle)** | 2024 | Seizure/harmful brain activity classification | 2,767 teams, $50K | [Kaggle](https://www.kaggle.com/competitions/hms-harmful-brain-activity-classification) |
| **CYBATHLON BCI Race** | 2024 | EEG-controlled avatar racing | International | [cybathlon.com](https://cybathlon.com/en/event/disciplines/bci) |
| **BCI Competition IV** | 2008+ | Motor imagery, SCP (ongoing benchmark) | Standard | [bbci.de](https://www.bbci.de/competition/iv/) |
| **BEETL (NeurIPS 2021)** | 2021 | Cross-subject/dataset transfer learning | 30+ teams | [beetl.ai](https://beetl.ai/challenge) |
| **International BCI Award** | Annual | Best BCI research project | $6K total | [bci-award.com](https://www.bci-award.com/Home) |

### 8.3 Conferences and Workshops

| Venue | Focus | Frequency |
|-------|-------|-----------|
| **IEEE EMBC** | Biomedical engineering (largest EEG venue) | Annual |
| **NeurIPS Brain-AI Workshop** | Brain-inspired AI, neural data + DL | Annual |
| **IEEE BCI Conference** | Brain-computer interface technology | Biennial |
| **OHBM** (Org. for Human Brain Mapping) | Neuroimaging (EEG + fMRI + MEG) | Annual |
| **SfN** (Society for Neuroscience) | All neuroscience | Annual |
| **ICASSP** | Signal processing (EEG sessions) | Annual |
| **EUSIPCO** | European signal processing | Annual |

---

## Part IX: Emerging Directions (2025-2027)

### 1. Multimodal EEG Fusion
Combining EEG with fMRI, MEG, or fNIRS using deep learning. EEG provides temporal resolution, fMRI provides spatial resolution. Recent: using LLMs (Gemma, Llama) to jointly process EEG and fMRI embeddings (2025).

### 2. Wearable and Consumer EEG
Dry-electrode headbands (Muse, IDUN Guardian, Emotiv Insight) approaching research quality. Market projected to reach $2.3B by 2027. Key challenge: signal quality vs. convenience tradeoff.

### 3. EEG Generative Models
- **EEGDM** (2025) — Diffusion model for generating synthetic EEG data. Applications: data augmentation, privacy-preserving EEG sharing.
- **EEGDfus** (2025) — Diffusion-based EEG denoising.

### 4. Real-Time AI Neurofeedback
Closed-loop systems where AI processes EEG in real-time and provides feedback to modify brain states. Applications: ADHD, anxiety, peak performance, meditation. Deep learning enables more sophisticated state detection than traditional band-power approaches.

### 5. Large-Scale Population EEG
Initiatives like HBN (3,000+ subjects) and UK Biobank (adding EEG) enable population-level brain studies. EEG brain age as a public health metric. Foundation models trained on these corpora may enable "universal" EEG encoders.

### 6. Privacy and Ethics
Brain data raises unique privacy concerns: neural signals may reveal sensitive information (cognitive states, psychiatric conditions, unspoken thoughts). Legal frameworks (e.g., Chile's "neurorights" law, 2021) are emerging. Technical solutions: federated learning for EEG, differential privacy for brain data.

---

## Contributing

This is a living document. Contributions welcome via pull requests. Please include proper citations for any added papers.

## License

This survey is released under [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/).

---

*Compiled 2026-04-10. If you find this useful, please star the repository.*
