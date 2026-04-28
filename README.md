# Genomic Evolution of Pseudomonas aeruginosa in Bronchiectasis. A Longitudinal WGS Analysis of Patients Under Cyclic Inhaled Ciprofloxacin Treatment

> MSc Bioinformatics Project · University of Liverpool  
> Author: On Zhao Xuan  
> Supervisors: Prof Steve Paterson · Dr Niamh Harrington


# Background
Non-cystic fibrosis bronchiectasis (NCFB) is a chronic respiratory condition characterised by permanent airway dilation and a self-perpetuating cycle of infection and inflammation. Over 60% of adult patients are colonised by bacterial pathogens, with *Pseudomonas aeruginosa* being the most clinically significant — linked to a three-fold increase in mortality and accelerated lung function decline. Its capacity for rapid genomic adaptation makes it exceptionally difficult to eradicate.

Inhaled liposomal ciprofloxacin (ARD-3150), delivered in a cyclic 28-days-on/28-days-off regimen, demonstrated clinical efficacy in the ORBIT-3 and ORBIT-4 phase 3 trials (Haworth et al., 2019). However, resistance was assessed solely by minimum inhibitory concentration (MIC) — a phenotypic measure that cannot reveal which genomic changes drive adaptation. Harrington et al. (2024) later characterised baseline *P. aeruginosa* diversity across bronchiectasis patients, identifying recurrently mutated genes such as *dnaX* and *femR*, but this cross-sectional snapshot cannot track how allele frequencies shift in response to oscillating antibiotic pressure. No study has applied longitudinal whole-genome SNP analysis to these populations.


# Research Question

> Does cyclic inhaled ciprofloxacin drive measurable, treatment-linked genomic evolution in *P. aeruginosa* — and do resistance mutations fluctuate with the 28-day ON/OFF cycle in a manner distinct from natural drift in untreated patients?

# Hypothesis: 
Cyclic ciprofloxacin treatment exerts oscillating positive selection on resistance loci (*gyrA*, *parC*), driving allele frequency increases during ON phases with partial reversals during OFF phases reflecting fitness costs — producing a trajectory of genomic adaptation distinct from neutral drift in placebo patients.


# Dataset
| Genomes sequenced | 280 WGS isolates |
| Patients (complete sampling) | 5 treatment + placebo controls |
| Timepoints | 9 across 48 weeks |
| Sequencing platform | Illumina NovaSeq · 150bp paired-end |
| Phylogenetic group | All isolates confirmed Group 1 |
| Reference genome | PAO1 (*P. aeruginosa*) |

## Pipeline Overview

Raw reads (FASTQ)
      │
      ▼
01  QC & Trimming         FastQC · MultiQC
      │
      ▼
02  De novo Assembly       Unicycler (normal mode, 500bp min)
      │
      ▼
03  Assembly QC            BUSCO (bacteria_odb10)
      │
      ▼
04  Genome Annotation      Bakta
      │
      ▼
05  Pangenome              Panaroo · snp-sites
      │
      ▼
06  Phylogeny              IQ-TREE (GTR+ASC, 1000 bootstrap)
      │
      ▼
07  AMR Detection          CARD · RGI
      │
      ▼
08  Variant Calling        Snippy · SnpEff          [upcoming]
      │
      ▼
09  Statistical Analysis   R · AMOVA · allele freq  [upcoming]

