# Homology Modelling of the Human MAS1 Receptor

**Author:** Jonatan Bella
**Date:** December 2024

A structural bioinformatics project building and validating a homology model of the human **proto-oncogene MAS1 receptor (MAS1)** — a Class A G-Protein Coupled Receptor (GPCR) of therapeutic interest as a natural antagonist of the AT1 receptor in the renin–angiotensin system, making it a relevant target for cardiovascular disease (notably hypertension).

---

## Overview

As of December 2024, MAS1 had no publicly available experimentally resolved structure, so its 3D architecture had to be inferred computationally. This project starts from the 325-aa UniProt target sequence, reconstructs a 323-residue comparative model of MAS1 from evolutionary and structural templates, validates its geometry against community-standard criteria, and benchmarks it against state-of-the-art deep-learning predictors (AlphaFold 2 and AlphaFold 3).

The resulting model recovers all seven transmembrane helices in an **active-state conformation**, including the characteristic outward tilt of TM6, conserved proline-induced kinks, and an amphipathic ICL2 helix — structural hallmarks known from the MAS-related GPCR (MRGPR) family.

## Pipeline

The workflow combines sequence-based template discovery, structural curation, comparative modelling, refinement, and multi-source validation:

1. **Target sequence acquisition** — UniProt entry retrieval for the human MAS1 receptor (325 aa).
2. **Template identification** — PSI-BLAST (BLOSUM62, 2 iterations) against the PDB, cross-matched with HHPRED profile-HMM searches to capture distant homologs.
3. **Template curation** — Filtering by sequence identity (≥20%, ≥84% query coverage), structural completeness (ECL1/ECL2 resolution), activation state, ligand presence, and phylogenetic proximity within the MRGPR family. Final templates: **8JGF, 7VV5, 8I95, 8YRG**.
4. **Homology model generation** — Multi-template comparative modelling with **MODELLER**.
5. **Secondary-structure cross-validation** — Transmembrane helix boundaries compared against **PSIPRED, MEMSAT-SVM, DeepTMHMM,** and UniProt annotations.
6. **Geometric validation** — **PROCHECK**, Ramachandran and Chi1-Chi2 plot analysis of all 323 residues.
7. **Loop refinement** — ICL3 remodelled with **ModLoop** and compared residue-by-residue against the Modeller-generated loop using interaction analysis (H-bonds, hydrophobic, π–π, CH–π).
8. **Benchmarking** — Pairwise alignment (RMSD, TM-score) of the refined model against **AlphaFold 2** and **AlphaFold 3** predictions, interpreted alongside pLDDT and PAE confidence scores.

## Key Results

- **Final model:** 323 modeled residues from a 325-aa MAS1 target sequence, preserving an active-state GPCR fold with all seven TM helices well defined.
- **Ramachandran quality:** **93.7% core / 5.0% allowed / 1.0% generous / 0.3% disallowed** — the four flagged residues lie exclusively in flexible loop regions (N-terminus, ECL2, ECL3), which is the expected profile for regions poorly resolved even in the crystal templates.
- **Structural hallmarks recovered:**
  - Outward-displaced TM6 at the cytoplasmic side — consistent with an active GPCR-like conformation.
  - Proline-induced kinks in TM6 and TM7, matching conserved activation motifs in the MRGPR family.
  - Amphipathic helix in ICL2 (PRO–ILE–TRP–TYR–ARG–CYS), positioned for G-protein coupling.
- **ModLoop vs. Modeller ICL3:** Side-by-side interaction mapping produced 6 stabilizing contacts for ModLoop (3 H-bonds, 2 hydrophobic, 1 π–π) vs. a more uniform but less-stabilizing Modeller loop — ModLoop selected as final refinement.
- **AlphaFold benchmark:** TM-score ≈ **0.70–0.71** across AF2/AF3 runs, indicating consistent overall fold prediction. Divergences concentrate in N/C termini and loops, precisely where AlphaFold's pLDDT confidence is lowest.

## Files

| File | Description |
|------|-------------|
| `finalterm_jonatan_bella.pdf` | Full 48-page technical report with methodology, figures, and per-residue analysis |
| `models/output (1).pdb` | Final refined homology model (post-ModLoop) |
| `models/modeller_6182805 (3).pdb` | Initial Modeller-generated model (pre-loop refinement) |

## Tools & Software

**Modelling & refinement:** MODELLER, ModLoop
**Sequence & template search:** PSI-BLAST (NCBI), HHPRED
**Secondary-structure prediction:** PSIPRED, MEMSAT-SVM, DeepTMHMM
**Validation:** PROCHECK, Ramachandran/Chi1-Chi2 analysis
**Deep-learning benchmark:** AlphaFold 2, AlphaFold 3
**Visualisation:** PyMOL, Modeller 3D viewer, RCSB PDB 3D viewer, LiteMol
**Databases:** UniProt, RCSB PDB

## Skills Demonstrated

- End-to-end structural bioinformatics pipeline design
- GPCR biology: activation mechanisms, TM topology, MRGPR family phylogeny
- Template selection strategy balancing identity, coverage, resolution, activation state and ligand state
- Critical interpretation of validation outputs (Ramachandran, PROCHECK, pLDDT, PAE, TM-score, RMSD)
- Comparative analysis between classical homology modelling and modern deep-learning predictors
- Residue-level structural reasoning (H-bonds, salt bridges, hydrophobic packing, π–π / CH–π interactions)
- Scientific writing and presentation of computational structural biology results

---

*For a complete, figure-rich walkthrough of each step — including visual checks of every template, TM helix, kink, side-chain interaction, and full literature citations — see the accompanying PDF report.*
