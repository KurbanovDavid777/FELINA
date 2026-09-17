# Data

| File | Rows | Description |
|---|---|---|
| `data_train.csv` | 834 | Curated reference set of bimetallic Fe complexes from COD (Fe + at most one other metal). One row per normalized COD ID. |
| `chemberta_embeddings.parquet` | — | ChemBERTa (`DeepChem/ChemBERTa-100M-MLM`) mean-pooled embeddings of component SMILES, keyed by `cod_id`. |
| `virtual_library.csv` | 20 | Laboratory-accessible candidate complexes P01–P20. |
| `top_10.csv` | 10 | Candidates with the lowest mean rank across the 80-model ensemble. |

## `data_train.csv` columns

| Group | Columns | Notes |
|---|---|---|
| Identifiers | `cod_id`, `cod_norm`, `source`, `type`, `formula_sum`, `smiles`, `metal_group` | `cod_norm` = COD ID without prefix/leading zeros; `metal_group` ∈ Fe-Fe, Fe-Co, Fe-Ni, Fe-Cu, Fe-Mn, Fe-Zn, Fe-Mo, Fe-Ba |
| Composition | `n_C` … `n_Br`, `*_per_Fe`, `has_<Metal>`, `is_homo`, `DBE`, `H_C_ratio`, `N_C_ratio`, `O_N_ratio` | from empirical formula |
| Donor atoms (HSAB) | `n_hard`, `n_soft`, `hard_soft`, `donors_per_Fe`, `n_heavy` | |
| Second metal | `M_radius`, `M_EN`, `M_d_elec`, `M_hardness`, `delta_EN`, `delta_radius` | differences relative to Fe |
| Magpie | `MagpieData *` | matminer elemental statistics |
| Geometry | `geo_*` | Fe coordination number, bond lengths, Fe–M distance, bridges (from crystal structures; not defined for hypothetical candidates) |
| Embeddings | `chemberta_0` … `chemberta_767` | |
| Other | `label` | constant, not used for training (models are unsupervised) |

Metal-pair counts: Fe-Fe 618, Fe-Co 54, Fe-Ni 46, Fe-Cu 42, Fe-Mn 37, Fe-Zn 19, Fe-Mo 14, Fe-Ba 4.

## `virtual_library.csv` columns

`ID`, `Status`, `Fe_oxidation_state`, `Family` (ligand), `Second_metal`, `Counterion`, `Gross_formula` (incl. crystallization water), `Ligand_formula`, `SMILES_complex` (with water), `SMILES_nowater` (used for embedding).

## Source and license

Derived from the [Crystallography Open Database](https://www.crystallography.net/cod/) (public domain), accessed April 2026. Released under CC BY 4.0 (see `LICENSE`).
