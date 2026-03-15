# NVIDIA BioNeMo

NVIDIA BioNeMo is an open developer platform for AI-driven life science research. 

It provides GPU-accelerated models, tools, and datasets for the entire AI lifecycle, enabling researchers and developers to build, customize, and deploy AI applications that transform physical lab results into the digital insights that drive the next experiment.

The platform is built on five core pillars:

* **Data:** Large-scale datasets for training, fine-tuning, and benchmarking models.
* **Models:** Open-source models for understanding biological systems, designing novel proteins and small molecules, and optimizing candidates for synthesizability, binding affinity, and molecular properties.
* **Libraries and Tools:** Foundational GPU-optimized libraries and kernels for accelerated AI training and inference.
* **Training and Customization:** Frameworks and recipes for pretraining, fine-tuning, and adapting models for specialized use cases.
* **Optimized Inference and Deployment:** Enterprise-ready NVIDIA inference microservices (NIM) and reference architectures for production use.


> **Note:** Many components of the BioNeMo platform are modular and hosted in their own dedicated GitHub repositories or organizations. This README serves as a central index to guide you to the right tools.

## Table of Contents

- [License](#license)
- [Data](#data)
- [Models](#models)
- [Libraries and Tools](#libraries-and-tools)
- [Training and Customization](#training-and-customization)
- [Optimized Inference and Deployment](#optimized-inference-and-deployment)
- [Workflow Examples and Community Contributions](#workflow-examples-and-community-contributions)

---

## License

BioNeMo components are generally released under:

* **Data:** CC BY 4.0 license
* **Model weights:** [NVIDIA Open Model License Agreement](https://www.nvidia.com/en-us/agreements/enterprise-software/nvidia-open-model-license/)
* **Code:** Apache 2.0 license

Individual components may vary — check each resource for specific license terms.

---

## Data

Unlike natural language models trained on internet-scale data, biology and chemistry lack the critical mass of data required for large, general-purpose foundation models. To address this ecosystem-wide gap, NVIDIA is partnering with leading organizations to create and release open datasets.

| Dataset | Description |
| :------ | :---------- |
| [3D Structures of Protein Complexes<br>(available through the AlphaFold Database)](https://alphafold.ebi.ac.uk/) | Large-scale open database of predicted protein complex structures built with ecosystem partners to accelerate interaction biology and drug discovery. License: CC BY 4.0 |
| [Consistency Distilled Synthetic Protein Database](https://catalog.ngc.nvidia.com/orgs/nvidia/teams/clara/resources/proteina-atomistica_data?version=release) | 455K curated, high-quality protein sequence-structure pairs. Built using ProteinMPNN to generate synthetic sequences for Foldseek AFDB cluster representative structures, then refolded with ESMFold to obtain fully atomistic, self-consistent models. Filtered to pLDDT > 80. License: CC BY 4.0 |

---

## Models

NVIDIA BioNeMo provides high-quality, fully open-source models — including the full training codebase, pre-trained weights, and research papers — completely free to use. These models are hosted in the [NVIDIA-Digital-Bio](https://github.com/NVIDIA-Digital-Bio) GitHub organization.

These models reflect our active research directions, and we highly encourage community feedback, collaboration, and adaptation to push their capabilities further.

### Understand

| Use Case | Model | Description |
| :------- | :---- | :---------- |
| Target Identification / Disease Understanding (RNA) | [CodonFM](https://github.com/NVIDIA-Digital-Bio/CodonFM) | Codon-level RNA foundation model trained on 130M protein-coding sequences from 22K+ species. Captures synonymous codon variation for mRNA design, stability modeling, and variant interpretation. |
| Structure Prediction (RNA) | [RNAPro](https://github.com/NVIDIA-Digital-Bio/RNAPro) | State-of-the-art RNA 3D structure prediction model. Combines Protenix-based co-folding architectures with RNA foundation models, MSA, and template-based modeling. |

### Design

| Use Case | Model | Description |
| :------- | :---- | :---------- |
| Proteins | [Proteina-Complexa](https://github.com/NVIDIA-Digital-Bio/Proteina-Complexa) | Protein binder design for protein and small molecule targets. Combines a pretrained flow-based generative model (built on La-Proteina) with inference-time optimization for high-quality binder generation. |
| | [La-Proteina](https://github.com/NVIDIA-Digital-Bio/la-proteina) | All-atom protein generation using partially latent flow matching. Jointly generates amino acid sequence and full atomistic structure (backbone + side chains) for up to 800 residues. Enables atomistic motif scaffolding for enzyme design. |
| | [Proteina](https://github.com/NVIDIA-Digital-Bio/proteina) | Large-scale flow-based generative model for protein backbone structures with hierarchical fold-class conditioning and a scalable transformer architecture. |
| | [ProtComposer](https://github.com/NVlabs/protcomposer) | Spatial-layout-conditioned protein structure generation using 3D ellipsoids to control shape and substructure arrangements. |
| Small Molecules | [GenMol](https://github.com/NVIDIA-Digital-Bio/genmol) | Fragment-based molecule generation using masked discrete diffusion over SAFE representations. Supports de novo design, scaffold decoration, linker design, motif extension, and lead optimization. |
| | [Megalodon](https://github.com/NVIDIA-Digital-Bio/megalodon) | Transformer-based 3D molecule generative model using equivariant graph transformer architecture. Generates both 2D topology and 3D structure with physically realistic, low-energy conformations. |
| | [AvgFlow](https://github.com/NVIDIA-Digital-Bio/avgflow) | Efficient molecular 3D conformer generation using SO(3)-averaged flow-matching and reflow. Architecture-agnostic framework applicable to equivariant and non-equivariant models. |

### Optimize

| Use Case | Model | Description |
| :------- | :---- | :---------- |
| Property Prediction | [KERMT](https://github.com/NVIDIA-Digital-Bio/KERMT) | Pretrained graph neural network for molecular property prediction (ADMET). Multi-task extension of GROVER with accelerated data loading via cuik-molmaker. SOTA on real-world ADMET data. |
| Synthesizability | [ReaSyn](https://github.com/NVIDIA-Digital-Bio/ReaSyn) | Synthesis pathway prediction using an encoder-decoder Transformer with Chain-of-Reaction notation. Predicts reaction steps from building blocks to final products, or finds synthesizable analogs for unsynthesizable targets. |
| Binding Energy | [DualBind](https://github.com/NVIDIA-Digital-Bio/dualbind) | 3D structure-based deep learning model for protein-ligand binding affinity prediction using a dual-loss framework (supervised MSE + unsupervised denoising). Orders of magnitude faster than physics-based FEP methods. |

---

## Libraries and Tools

GPU-optimized libraries and tools that integrate into existing workflows. Engineered to be lightweight and specialized for maximum performance without dependency bloat.

| Task | Tool | Description |
| :--- | :--- | :---------- |
| Data Processing & Analysis | [Parabricks](https://github.com/clara-parabricks-workflows) | GPU-accelerated genomics software suite for rapid secondary analysis of DNA/RNA sequencing data. |
| | [nvMolKit](https://github.com/NVIDIA-Digital-Bio/nvMolKit) | GPU-accelerated cheminformatics library for molecular fingerprinting, Tanimoto/cosine similarity, Butina clustering, conformer generation (ETKDGv3), MMFF geometry optimization, and substructure search. |
| | [cuik-molmaker](https://github.com/NVIDIA-Digital-Bio/cuik-molmaker) | Molecular featurization package for converting chemical structures into GNN inputs. Accelerates Chemprop training by 1.6x and inference by 2.4x with 80% memory reduction. |
| | [nvQSP](https://github.com/NVIDIA-Digital-Bio/nvQSP) | GPU-accelerated Quantitative Systems Pharmacology ODE solvers. 77x speedup over CPU for virtual patient simulations with bit-exact FP64 reproducibility. |
| Training & Inference | [cuEquivariance](https://github.com/NVIDIA/cuEquivariance) | CUDA-X library with optimized kernels for efficient training of geometry-aware equivariant neural networks (AlphaFold-like and molecular structure models). |
| | [BioNeMo-SCDL](https://github.com/NVIDIA/bionemo-framework) | Scalable, memory-efficient data loader for training large single-cell models. Part of BioNeMo Framework. |
| | [BioNeMo-MoCo](https://github.com/NVIDIA/bionemo-framework) | Framework for constructing generative models (diffusion, flow-matching) using continuous and discrete interpolants. Part of BioNeMo Framework. |
| | [BioNeMo-Noodles](https://github.com/NVIDIA/bionemo-framework) | Efficient genomic data handling with memory-mapped access to FASTA files. Part of BioNeMo Framework. |

---

## Training and Customization

BioNeMo provides frameworks and recipes for pretraining, fine-tuning, and adapting biomolecular AI models at scale on GPU infrastructure.

| Tool | Description |
| :--- | :---------- |
| [BioNeMo Framework](https://github.com/NVIDIA/bionemo-framework) | Reference training implementations and ready-to-run examples showing how to achieve lower-precision training, maximum scaling & throughput for models like Llama3, ESM2, Evo2, CodonFM, and Geneformer using FSDP and TransformerEngine. |
| [Context Parallelism (boltz-cp)](https://github.com/NVIDIA-Digital-Bio/boltz-cp) | Long-sequence parallelism for protein structure prediction models. Distributes activation tensors across GPUs to overcome single-GPU memory limits for large biomolecules. |

Documentation: [docs.nvidia.com/bionemo-framework](https://docs.nvidia.com/bionemo-framework/)

---

## Optimized Inference and Deployment

BioNeMo NIM microservices are enterprise-ready inference microservices with built-in API endpoints. Each NIM includes algorithmic, system, and runtime optimizations into a prebuilt container — go from zero to inference in minutes.

| NIM | Description |
| :-- | :---------- |
| [OpenFold3](https://build.nvidia.com/openfold/openfold3) | 3D structure prediction for molecular complexes (proteins, DNA, RNA, ligands) |
| [OpenFold2](https://build.nvidia.com/openfold/openfold2) | Protein structure prediction from sequence, MSAs, and templates |
| [Boltz-2](https://build.nvidia.com/mit/boltz2) | Biomolecular complex structure prediction |
| [Evo2-40B](https://build.nvidia.com/arc/evo2-40b) | Genomic foundation model with long-context sequence understanding |
| [MSA Search](https://build.nvidia.com/colabfold/msa-search) | Multiple sequence alignment generation from query sequences |
| [ProteinMPNN](https://build.nvidia.com/ipd/proteinmpnn) | Amino acid sequence design for protein backbones |
| [RFDiffusion](https://build.nvidia.com/ipd/rfdiffusion) | Generative model for protein backbone and binder design |
| [GenMol](https://build.nvidia.com/nvidia/genmol-generate) | Fragment-based small molecule generation |
| [DiffDock](https://build.nvidia.com/mit/diffdock) | Molecular blind docking for predicting protein-ligand binding poses |
| [MolMIM](https://build.nvidia.com/nvidia/molmim-generate) | Molecular generation optimized for user-defined drug properties |

Browse all available NIM microservices: [build.nvidia.com/explore/biology](https://build.nvidia.com/explore/biology)

NIM microservices can be deployed self-hosted via Docker or Kubernetes, or on cloud platforms including AWS, Google Cloud, Microsoft Azure, and NVIDIA DGX Cloud.

---

## Workflow Examples and Community Contributions

Application-level examples showing how BioNeMo platform components work together:

* [**digital-biology-examples**](https://github.com/NVIDIA/digital-biology-examples) — End-to-end workflow examples for drug discovery and biological research.

> **Note:** If you have an example you'd like to contribute, we'd love to include it. Please get started by opening a GitHub issue and we'll reach out to you.
