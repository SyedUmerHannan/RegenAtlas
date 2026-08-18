# RegenAtlas: Cross-Species Mining of Cardiac Regeneration Programs

**Cross-species mining of cardiac regeneration programs from public single-cell data.**

---

## 📌 Project Overview

**RegenAtlas** leverages existing public single-cell and single-nucleus RNA-sequencing (sc/snRNA-seq) datasets from regeneration-competent and regeneration-incompetent hearts. The goal is to identify a prioritized, defensible hypothesis list of conserved regulatory programs that gate cardiomyocyte (CM) proliferation across species for wet-lab validation.

Rather than searching for a single master switch, this project tests the hypothesis that the regenerative phenotype consists of a small set of convergent programs—such as cell-cycle re-entry, sarcomere disassembly, dedifferentiation TFs, and a permissive metabolic state—that are lost in a specific, identifiable order as regenerative competence closes.

> **Disclaimer & Framing:** This repository produces a prioritized triage list for wet-lab follow-up; it is a hypothesis generator rather than an independent mechanistic proof or discovery claim.

---

## 🔬 Target Species & Datasets (Module I)

RegenAtlas integrates datasets across multiple species spanning regenerative and non-regenerative boundaries[cite: 1]:

* **Zebrafish (Fully Regenerative, Adult & Larval)**[cite: 1]
  * `GSE145982`: Non-myocyte single-cell atlas across a regeneration time course (~62k cells)[cite: 1].
  * `GSE262689`: Comparative single-cell profiling across zebrafish, medaka, and mouse[cite: 1].
  * `GSE130487`: Zebrafish cell landscape atlas for general annotation[cite: 1].
* **Neonatal Mouse (Regenerative Window Closes ~P7)**[cite: 1]
  * `GSE130699`: Cui et al. 2020 snRNA-seq of CMs at P1 vs. P8 (sham vs. MI, 1 & 3 dpi)[cite: 1].
  * Companion scATAC-seq (Cell Reports 2020) for TF accessibility cross-checks[cite: 1].
  * `MCAREDB`: Harmonized Seurat object integrating three published neonatal mouse datasets[cite: 1].
* **Adult Mouse (Non-Regenerative / Within-Species Control)**[cite: 1]
  * `GSE136088`: Interstitial cells post-MI/sham[cite: 1].
  * `GSE132880`: Endothelial transcriptomes post-MI[cite: 1].
  * Adult mouse CM-specific post-MI single-nucleus RNA-seq datasets[cite: 1].
* **Human (Non-Regenerative / Clinically Relevant)**[cite: 1]
  * **Human Heart Cell Atlas** (Litviňuková et al. 2020, `ERP123138`): Baseline healthy adult heart atlas[cite: 1].
  * **Heart Failure Atlas** (Koenig et al. 2022): Diseased/injured non-regenerating human comparator[cite: 1].
* **Pig (Large Mammal / Translational Bridge)**[cite: 1]
  * Published snRNA-seq dataset comparing P1 apical resection (heals without scarring) vs. P28 MI (scarring) and fetal controls[cite: 1].

---

## 🏗️ Technical Pipeline & Modules

flowchart TD
    M1["**Module I: Data Aggregation**"] 
    M2["**Module II: Cross-Species Integration & Validation**"] 
    M3["**Module III: Trajectory & Cell-State Analysis**"] 
    M4["**Module IV: Regulatory Network Comparison**"] 
    M5["**Module V: Candidate Prioritization Triage**"] 
    M6["**Module VI: Boolean Model (Stretch Goal)**"]

    T2["SAMap, Ensembl Compara, Harmony / scVI"]
    T3["Cell-Cycle Scoring, Pseudotime, Sarcomere Disassembly"]
    T4["pySCENIC Regulon Inference, scATAC Cross-Checking"]
    T5["Scoring (Consistency, Evidence, Druggability, Directionality)"]
    T6["Optional qualitative logic consistency check"]

    M1 --> M2 --> M3 --> M4 --> M5 --> M6

    T2 -.-> M2
    T3 -.-> M3
    T4 -.-> M4
    T5 -.-> M5
    T6 -.-> M6


1. **Module I - Data Aggregation**: Per-species independent QC, standard filtering (genes/cell, mitochondrial %, doublets), and metadata harmonization.
2. **Module II - Cross-Species Integration**:
   * Baseline ortholog mapping using Ensembl Compara (1-to-1, 1-to-many, many-to-many).
   * Within-species harmonization using `Harmony` or `scVI`.
   * Cross-species graph-based mapping using `SAMap`.
   * Validation of integration using conserved cell markers (`TNNT2`, `MYH6/7`, `PECAM1`, `COL1A1`).
3. **Module III - Trajectory & Cell-State Analysis**
   * Cell-cycle scoring and sarcomere disassembly signature tracking.
   * Pseudotime trajectory inference (e.g., `Monocle3`, `Slingshot`, or `scVelo`) along injury-response axes.
   * Differential expression between matched timepoints across regenerative boundaries.
4. **Module IV - Regulatory Network Comparison**:
   * Transcription factor regulon inference using `pySCENIC`.
   * Integration with matched mouse scATAC-seq data.
   * Pipeline sanity checks against known literature regulators (e.g., Hippo/YAP, Meis1, Tbx20, Nrg1/ErbB4, Cyclin D2).
5. **Module V - Candidate Prioritization**:
   * Multi-factorial scoring system based on:
     1. Cross-species consistency.
     2. Literature perturbation evidence.
     3. Druggability and clinical tractability.
     4. Direction-of-effect consistency across species.
6. **Module VI - Boolean Logic Model (Optional Stretch Goal)**:
   * Qualitative dynamic modeling of top 5–10 regulators via `BoolNet` or `PyBoolNet` to confirm internal logic consistency.

---

## 🛠️ Tooling & Tech Stack

* **Python**: `Scanpy`, `scVI`, `SAMap`, `pySCENIC`, `scVelo`.
* **R**: `Seurat`, `Harmony`, `Monocle3`, `Slingshot`, `BoolNet`.
* **Reference Databases**: Ensembl Compara, cisTarget motif databases.
* **Compute Environment**: High-performance computing cluster / High-memory cloud resources.

---

## ⚠️ Known Limitations & Explicit Caveats

* **Association vs. Causation**: Transcriptomic and regulon conservation points to hypotheses, not proven drivers of regeneration[cite: 1].
* **Cross-Species Integration Artifacts**: Potential batch effects across technologies (10x vs. Smart-seq, snRNA vs. scRNA) and ortholog mapping ambiguities[cite: 1].
* **Injury Model Heterogeneity**: Compares distinct physiological stimuli across species (e.g., apical resection vs. cryoinjury vs. coronary ligation MI)[cite: 1].
* **RNA Proxy Limits**: RNA expression serves as an incomplete proxy for protein-level and structural dynamics, particularly for sarcomere disassembly[cite: 1].

---

## 📅 Milestones & Timeline

| Timeline | Phase | Description |
| :--- | :--- | :--- |
| **Month 0–1** | Setup & Benchmark | Environment setup; reproduce zebrafish/mouse comparison (`GSE262689`) as pipeline milestone[cite: 1]. |
| **Month 1–2** | Module I | Data download, QC, and metadata harmonization across species[cite: 1]. |
| **Month 2–4** | Module II & III | Ortholog mapping, SAMap cross-species integration, pseudotime & trajectory analysis[cite: 1]. |
| **Month 4–6** | Module IV | `pySCENIC` regulon inference per dataset and cross-species TF matrix assembly[cite: 1]. |
| **Month 6–9** | Module V | Scoring framework execution and ranked candidate table generation[cite: 1]. |
| **Month 9–10** | Module VI | *(Optional)* Boolean dynamic model construction[cite: 1]. |
| **Month 10–12**| Finalization | Manuscript preparation, code documentation, and collaborator sanity-checks. |

---

## 📚 Key References

* **Cui et al. 2020** (*Dev Cell* / *Cell Rep*): Murine neonatal CM single-nucleus RNA-seq & scATAC-seq datasets (`GSE130699`)[cite: 1].
* **Litviňuková et al. 2020** (*Nature*): Adult Human Heart Cell Atlas (`ERP123138`)[cite: 1].
* **Koenig et al. 2022** (*Nat Cardiovasc Res*): Human heart failure single-cell atlas[cite: 1].
* **Tarashansky et al. 2021** (*eLife*): SAMap cross-species single-cell atlas mapping[cite: 1].
* **Luecken et al. 2023** (*Nat Commun*): Cross-species scRNA-seq integration benchmark[cite: 1].
* **Aibar et al. 2017** (*Nat Methods*): SCENIC regulatory network inference[cite: 1].
* **Porrello et al. 2011**: Neonatal mouse regenerative window[cite: 1].
