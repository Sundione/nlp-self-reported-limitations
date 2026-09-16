# NLP Limitations with Human Qualitative Coding

150 papers sampled from the ACL Anthology (2020–2025). Each record holds the paper identifier, title, abstract, the verbatim Limitations section, and that section split into numbered sentences, with human qualitative codes attached: codes drawn from an established codebook, and codes the annotators created where no existing code fitted the statement. Independently coded by four expert annotators and reconciled to consensus — built as a human reference standard.

**Data card:** [data_card.md](data_card.md) · [data_card.pdf](data_card.pdf)

## Files

| File | Contents |
|---|---|
| [`human_code.csv`](human_code.csv) | 150 papers: `paper_id`, `title`, `abstract`, `limitation`, `segmented_text`, `existing_code`, `new_code` |
| [`codebook_initial.csv`](codebook_initial.csv) | The 25-code codebook the annotators worked from (`Code Name`, `Code Definition`) |

See the [repository root README](../README.md) for how this dataset relates to the companion [`llm_coded_dataset/`](../llm_coded_dataset/).
