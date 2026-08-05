# RegenAtlas: Cross-Species Mining of Cardiac Regeneration Programs

**Cross-species mining of cardiac regeneration programs from public single-cell data[cite: 1].**

---

## 📌 Project Overview

**RegenAtlas** leverages existing public single-cell and single-nucleus RNA-sequencing (sc/snRNA-seq) datasets from regeneration-competent and regeneration-incompetent hearts[cite: 1]. The goal is to identify a prioritized, defensible hypothesis list of conserved regulatory programs that gate cardiomyocyte (CM) proliferation across species for wet-lab validation[cite: 1].

Rather than searching for a single master switch, this project tests the hypothesis that the regenerative phenotype consists of a small set of convergent programs—such as cell-cycle re-entry, sarcomere disassembly, dedifferentiation TFs, and a permissive metabolic state—that are lost in a specific, identifiable order as regenerative competence closes[cite: 1].

> **Disclaimer & Framing:** This repository produces a prioritized triage list for wet-lab follow-up; it is a hypothesis generator rather than an independent mechanistic proof or discovery claim[cite: 1].

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
