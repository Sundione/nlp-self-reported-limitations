# NLP Limitations with LLM Qualitative Coding

Qualitative codes assigned by a large language model to the Limitations sections of 16,047 papers from the ACL Anthology (2020–2025). Every code assignment is traced to the sentences that triggered it, with a character span into the Limitations section and a short justification written by the model. All labels are machine-generated, for large-scale analysis rather than as a reference standard — see the companion [`human_coded_dataset/`](../human_coded_dataset/) for that.

**Data card:** [data_card.md](data_card.md) · [data_card.pdf](data_card.pdf)

## Files

Released as four year-group files, each in JSON (primary) and CSV, alongside the codebook version that round produced:

| Folder | Papers file | Codebook file (output of this round) |
|---|---|---|
| [`2020_2022/`](2020_2022/) | `papers_2020_2022.json` / `.csv` | `codebook_after_2022.csv` (47 codes) |
| [`2023/`](2023/) | `papers_2023.json` / `.csv` | `codebook_after_2023.csv` (47 codes) |
| [`2024/`](2024/) | `papers_2024.json` / `.csv` | `codebook_after_2024.csv` (48 codes) |
| [`2025/`](2025/) | `papers_2025.json` / `.csv` | `codebook_after_2025.csv` (50 codes, final) |

Note: the codebook file bundled in each folder is the version *produced after* that round — i.e. the one used to code the *next* year's file, not the one that folder's own papers file was coded against. See [data_card.md](data_card.md#dataset-snapshot--description-of-content) for the codebook-version-per-file mapping.

See the [repository root README](../README.md) for how this dataset relates to the companion [`human_coded_dataset/`](../human_coded_dataset/).
