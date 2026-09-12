# NLP Self-Reported Limitations

This repository is associated with an EMNLP 2026 Findings paper, titled **"What Limits Us? Analyzing Self-Reported Limitations in NLP Research"** `[TO FILL: paper / arXiv link]`, by Tawan Thaepprasit, Peeranuth Kehasukcharoen, Ding Wang, Remi Denton, Peerapon Vateekul, and Piyawat Lertvittayakumjorn.

## Abstract

This repository contains two companion datasets built from Limitations sections in the ACL Anthology (2020–2025): a 150-paper set independently coded by four expert human annotators, used as a reference standard, and a 16,047-paper set coded by a large language model with evidence spans and justifications tracing every code back to the sentence that triggered it. Both are coded against the same underlying codebook lineage, so the LLM-coded set can be evaluated directly against the human one. More details for each can be found in their respective data cards, linked below.

## Datasets

This repository also contains the codebook versions used to produce both datasets.

| Dataset | What it is | Scale | Data Card |
|---|---|---|---|
| [`human_coded_dataset/`](human_coded_dataset/) | 150 ACL Anthology papers (2020–2025), Limitations sections double/triple-coded by four expert annotators, used as a reference standard | 150 papers · 606 human labels | [data_card.md](human_coded_dataset/data_card.md) · [data_card.pdf](human_coded_dataset/data_card.pdf) |
| [`llm_coded_dataset/`](llm_coded_dataset/) | 16,047 ACL Anthology papers (2020–2025), Limitations sections coded by Gemini 3.1 Pro with evidence spans and justifications, for large-scale analysis | 16,047 papers · 84,930 code assignments | [data_card.md](llm_coded_dataset/data_card.md) · [data_card.pdf](llm_coded_dataset/data_card.pdf) |

The LLM-coded dataset is not a substitute for the human-coded one — it is evaluated *against* it (Krippendorff's alpha 0.644 among human annotators alone vs. 0.647 with the model added as a coder). See each dataset's data card for full detail, known caveats, and intended use.

## Repository Structure

```
.
├── README.md
├── human_coded_dataset/
│   ├── data_card.md            # data card, mirrored from the PDF below
│   ├── data_card.pdf            # original formatted data card
│   ├── codebook_initial.csv     # 25-code codebook the human annotators worked from
│   └── human_code.csv           # 150 papers, human-coded (existing_code / new_code)
└── llm_coded_dataset/
    ├── data_card.md
    ├── data_card.pdf
    ├── 2020_2022/
    │   ├── codebook_after_2022.csv
    │   ├── papers_2020_2022.csv
    │   └── papers_2020_2022.json
    ├── 2023/
    │   ├── codebook_after_2023.csv
    │   ├── papers_2023.csv
    │   └── papers_2023.json
    ├── 2024/
    │   ├── codebook_after_2024.csv
    │   ├── papers_2024.csv
    │   └── papers_2024.json
    └── 2025/
        ├── codebook_after_2025.csv
        ├── papers_2025.csv
        └── papers_2025.json
```

## Codebook Versioning

The codebook grew additively across the project — no code was ever removed once introduced:

| Version | Codes | Used to code |
|---|---|---|
| `codebook_initial` | 25 | `human_coded_dataset` (all 150 papers) and `llm_coded_dataset/2020_2022` |
| `codebook_after_2022` | 47 | `llm_coded_dataset/2023` |
| `codebook_after_2023` | 47 | `llm_coded_dataset/2024` |
| `codebook_after_2024` | 48 | `llm_coded_dataset/2025` |
| `codebook_after_2025` | 50 (final) | — final version, released for provenance |

The codebook CSV checked into each `llm_coded_dataset` year folder is the **output** codebook of that round — the version produced after coding that year-group, which then becomes the input for coding the *next* file in the table above. It is not the version that folder's own paper file was coded against; that version is documented in the table, not bundled in the same folder.

## Citation

If you use this dataset, please cite:

```
[TO FILL: BibTeX entry once the paper has a venue URL / DOI / pages]

@inproceedings{thaepprasit-etal-2026-what,
    title     = "What Limits Us? Analyzing Self-Reported Limitations in {NLP} Research",
    author    = "Thaepprasit, Tawan  and
                 Kehasukcharoen, Peeranuth  and
                 Wang, Ding  and
                 Denton, Remi  and
                 Vateekul, Peerapon  and
                 Lertvittayakumjorn, Piyawat",
    booktitle = "Findings of the Association for Computational Linguistics: EMNLP 2026",
    year      = "2026",
    address   = "[TO FILL]",
    publisher = "Association for Computational Linguistics",
    url       = "[TO FILL]",
    doi       = "[TO FILL]",
    pages     = "[TO FILL]"
}
```

## License

Released under [CC BY 4.0](LICENSE) ([human-readable summary](https://creativecommons.org/licenses/by/4.0/)), consistent with ACL Anthology practice for material published from 2016 onward. Attribution to the original paper authors for verbatim quoted text is carried by `paper_id` in both datasets.

Data card structure follows the [Data Cards Playbook](https://sites.research.google/datacardsplaybook/) by Google Research (CC BY-SA 4.0).

## Contact

- Tawan Thaepprasit — tawanth.official@gmail.com
- Peeranuth Kehasukcharoen — 6030416021@alumni.chula.ac.th
