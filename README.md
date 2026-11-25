# AcademicVault: deadline-constrained blockchain anchoring of academic certificates

Code and data for the paper "Batching, Timing and Learning in Deadline-Constrained
Blockchain Anchoring of Academic Certificates: A Walk-Forward Study".

The notebook compares policies for anchoring certificate hashes on Ethereum (Merkle
batching, fee-aware timing, ML forecasts, tabular Q-learning) under a 24-hour SLA,
using walk-forward evaluation on real Ethereum base-fee data.

## Files
| File | Content |
|---|---|
| `AcademicVault.ipynb` | Full pipeline: data loading, policies, experiments, self-tests, tables and figures |
| `ethereum_fee_5min_2024.csv` | 105,408 five-minute rows, 2024 |
| `ethereum_fee_5min_2025.csv` | 105,120 rows, 2025 |
| `ethereum_fee_5min_2026_jan_aug.csv` | 69,984 rows, Jan–Aug 2026 |
| `SHA256SUMS.txt` | Full SHA-256 hash of each CSV |
| `artifacts/` | (optional) result tables and figures produced by the notebook |

## Data
Source: Dune Analytics, table `ethereum.blocks` (DuneSQL), aggregated to five-minute
UTC intervals and downloaded on 27 September 2026. Columns: `interval_start`,
`avg_base_fee_gwei`, `avg_gas_utilization`, `blocks_in_interval`. The extraction SQL
is in Appendix A of the paper. Check files with `sha256sum -c SHA256SUMS.txt`.

## How to run
1. Install: `pip install scikit-learn pandas numpy matplotlib cryptography xgboost`
2. Keep the three CSVs in the same folder as the notebook.
3. Open `AcademicVault.ipynb` and run all cells (Jupyter or Google Colab).
   The full run is long (roughly 70+ minutes in our run). Outputs are written to `artifacts/`.

## Important limitations
Certificate arrivals are synthetic and gas costs per transaction are placeholders,
so results describe relative policy behaviour, not absolute cost.

## License
Code: MIT. Data: CC BY 4.0. See `LICENSE`.
