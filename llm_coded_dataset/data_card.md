# NLP Limitations with LLM Qualitative Coding — Data Card

**Data Card Authors:** Tawan Thaepprasit

The formatted, original version of this data card is available as [`data_card.pdf`](data_card.pdf). This file mirrors that PDF in Markdown.

This dataset is associated with an EMNLP 2026 Findings paper, titled *["What Limits Us? Analyzing Self-Reported Limitations in NLP Research"](https://arxiv.org/abs/2609.15191)*. The dataset contains qualitative codes assigned by a large language model to the Limitations sections of 16,047 papers from the ACL Anthology published between 2020 and 2025. Every code assignment is traced to the sentences that triggered it, with a character span into the Limitations section and a short justification written by the model. It is organised paper-first: the top level is the paper, and each record carries the codes assigned to it along with the evidence supporting each one. All labels are machine-generated; the dataset carries no human annotation and is intended for large-scale analysis of how limitation statements are reported, not as a reference standard. A companion dataset of 150 papers coded by four human annotators is released separately — see [`human_coded_dataset/`](../human_coded_dataset/).

## Dataset Team(s) / Contact / Authors

| Dataset Team(s) | Dataset Contact | Dataset Authors |
|---|---|---|
| Technology, AI, Society, and Culture (TASC) Team, Google<br>Data MIND Lab, Department of Computer Engineering, Faculty of Engineering, Chulalongkorn University | Tawan Thaepprasit: tawanth.official@gmail.com<br>Peeranuth Kehasukcharoen: 6030416021@alumni.chula.ac.th | Tawan Thaepprasit, Chulalongkorn University in Thailand<br>Peeranuth Kehasukcharoen, Chulalongkorn University in Thailand<br>Ding Wang, Google<br>Remi Denton, Google<br>Peerapon Vateekul, Chulalongkorn University in Thailand<br>Piyawat Lertvittayakumjorn, Google |

## Primary Data Modality / Dataset Snapshot / Description of Content

**Primary Data Modality**
- [ ] Image Data
- [x] Text Data
- [ ] Tabular Data
- [ ] Audio Data
- [ ] Video Data
- [ ] Time Series
- [ ] Graph Data
- [ ] Geospatial Data
- [ ] Multimodal
- [ ] Others
- [ ] Unknown

**Dataset Snapshot**

| Metric | Value |
|---|---|
| Size of dataset | 121.3 MB (JSON, primary) / 107.4 MB (CSV) |
| Number of instances | 16,047 papers across four files |
| Codes in the codebook | 50 |
| Code assignments | 84,930 |
| Evidence spans | 131,166 |
| Average codes per paper | 5.29 |
| Average spans per paper | 8.17 |
| Algorithmic labels | 84,930 |
| Human labels | 0 |

An assignment is one code applied to one paper. A paper carries between 1 and 19 codes, and between 1 and 62 evidence spans.

Released as four files, each in JSON (primary) and CSV, coded against the codebook version current when that year-group was processed. Codebook growth is additive: no code was removed once introduced, though three were renamed for clarity between the first two versions.

| File | Years | Papers | Codebook version (size) |
|---|---|---|---|
| `papers_2020_2022` | 2020–2022 | 1,595 | `codebook_initial` (25) |
| `papers_2023` | 2023 | 4,024 | `codebook_after_2022` (47) |
| `papers_2024` | 2024 | 4,159 | `codebook_after_2023` (47) |
| `papers_2025` | 2025 | 6,269 | `codebook_after_2024` (48) |

> **Note on file naming in this repository:** the codebook CSV checked into each year folder (e.g. [`2020_2022/codebook_after_2022.csv`](2020_2022/codebook_after_2022.csv)) is the **output** codebook of that round — produced at the end of coding that year-group, and used to code the **next** file in the table above. It is not the version that folder's own paper file was coded against; that version is named in the table, not bundled in the same folder. This is intentional: each folder pairs a year-group's papers with the codebook snapshot that round produced, which then becomes the input for the next round.

## Dataset Subject / Example Data Point / Data Fields

**Dataset Subject**
- [ ] Sensitive Data about people
- [ ] Non-Sensitive Data about people
- [ ] Data about natural phenomena
- [ ] Data about places and objects
- [x] Synthetically generated data
- [ ] Data about systems or products
- [x] Others: text published in academic proceedings
- [ ] Unknown

**Example: Data Point**

```
paper_id       2020.acl-main.189
title          Active Imitation Learning with Noisy Guidance
existing_code  ['Methodological Constraints', 'Non-Limitation: Anticipated Impact',
               'Non-Limitation: Method Details', 'Non-Limitation: Method Strength',
               'Non-Limitation: Strong Reported Performance']
new_code       []

existing_code_details[0].code_name                'Methodological Constraints'
  .evidence[0].segmented_id                        '2020.acl-main.189_s05'
  .evidence[0].segmented                           "1. In some settings, learning a difference
                                                     classifier may be as hard or harder than
                                                     learning the structured predictor; for
                                                     instance if the task is binary sequence
                                                     labeling (e.g., word segmentation),
                                                     minimizing its usefulness."
  .evidence[0].highlight_start / highlight_end      746 / 949
  .evidence[0].highlight_text                       "learning a difference classifier may be as
                                                     hard or harder than learning the structured
                                                     predictor; for instance if the task is binary
                                                     sequence labeling …"
  .evidence[0].justification                        "The authors identify a structural
                                                     vulnerability in their own methodology: the
                                                     internal component they rely on … can become
                                                     too difficult to learn in certain settings,
                                                     undermining the method's utility."
new_code_details  []
```

**Data Fields**

| Field | Type | Description |
|---|---|---|
| `paper_id` | str | ACL Anthology identifier, unique per record |
| `title` | str | paper title as published |
| `abstract` | str | paper abstract as published; empty for 4 of 16,047 records |
| `limitation` | str | verbatim Limitations section |
| `segmented_text` | str → dict[str, str] | JSON map of `sentence_id` to sentence, decoded with `json.loads` |
| `existing_code` | list[str] | codes matched to the codebook version this file was coded against |
| `new_code` | list[str] | codes created where no codebook entry fitted |
| `existing_code_details` | list[dict] | one entry per code in `existing_code`: `{code_name (str), evidence (list[dict])}` |
| `new_code_details` | list[dict] | same structure, for `new_code` |
| `evidence[].segmented_id` | str | key into `segmented_text` identifying which sentence this span falls within |
| `evidence[].segmented` | str | the text of that sentence, copied from `segmented_text[segmented_id]` |
| `evidence.highlight_start`, `highlight_end` | int | offsets into the full `limitation` string, not into any single sentence |
| `evidence.highlight_text` | str | the highlighted span |
| `evidence.justification` | str | mean 115 characters, min 12, max 419 |

**Note**: evidence entries carry no `sentence_id` field of their own name — linking a span back to a `segmented_text` entry requires matching its offset range against the sentence boundaries, since the two are not directly cross-referenced beyond `segmented_id`/`segmented` (see Reflections on Data below for the cases where the offsets themselves don't resolve).

## Dataset Purpose(s) / Key Domains or Application(s)

**Dataset Purpose(s)**
- [ ] Monitoring
- [x] Research
- [ ] Production
- [ ] Others

**Domains**: Natural language processing, qualitative coding methodology, meta-research on scholarly writing.

**Problem Space**: What NLP researchers report as the limitations of their own work, at a scale no manual coding effort could reach, and how that reporting shifts across venues and years.

## Dataset Usage / Intended and/or Suitable Use Case(s)

- [ ] Safe for production use
- [x] Safe for research use
- [ ] Conditional use
- [ ] Only approved use
- [ ] Others

- Large-scale analysis of which limitation categories are reported, and how that distribution moves across venues and years.
- Studying rhetorical strategy through the Non-Limitation codes, which mark content that sits in a Limitations section without being a limitation.
- Tracing a claim back to the sentence that produced it, using the evidence spans and justifications.

Unsuitable as ground truth. These are model judgements, not human ones. Where a reference standard is needed, use the companion human-coded dataset. Also unsuitable for year-on-year comparison without weighting, given the coverage imbalance described below.

## Safety of Use with Other Data / Acceptable Transformations

- [ ] Safe to use with other data
- [x] Conditionally safe to use with other data
- [ ] Should not be used with other data
- [ ] Unknown

Acceptable transformations: [x] Joining with other datasets · [x] Subsampling and splitting · [x] Filtering · [ ] Joining input sources · [ ] Cleaning missing values · [ ] Anomaly detection · [x] Grouping and summarizing · [ ] Scaling and reducing · [ ] Statistical transformations · [ ] Redaction or Anonymization

Join on `paper_id`, which resolves against ACL Anthology metadata. Pivoting the file from code-first to paper-first is the usual first step, since most analyses are per paper.

## Version Status / Dataset Version / Maintenance Plan

- [ ] Regularly Updated
- [ ] Actively Maintained
- [x] Limited Maintenance
- [ ] Deprecated

| | |
|---|---|
| Last Updated | Jun 2026 |
| Release Date | Aug 2026 |

The codebook itself went through several versions, revised annually with humans in the loop as new material was coded. All versions are released, and the 50-code codebook documented here is the final one.

**Maintenance plan**: The dataset is a fixed output of one coding run. No expansion is planned, but errors will be corrected if they surface.

## Access Policy / Retention Policy / Wipeout Policy

**Access Policy**: Public. Released under CC BY 4.0 in the same GitHub repository as the codebook versions and the companion human-coded dataset.

Repository: https://github.com/Sundione/nlp-self-reported-limitations

CC BY 4.0 follows ACL Anthology practice for material published from 2016 onward. Attribution to the original paper authors is required for the quoted sentences and is carried by `paper_id`.

**Retention Policy**: No retention limit. The dataset is intended to remain available as a fixed record of the coding run, and contains no personal data.

**Wipeout Policy**: Not applicable. No deletion schedule applies.

## Data Collection Methods / Data Sources / Data Collection

**Data Collection Methods**
- [ ] API
- [x] Artificially Generated
- [ ] Crowdsourced – Paid
- [ ] Crowdsourced – Volunteer
- [ ] Vendor Collection Efforts
- [x] Scraped or Crawled
- [ ] Survey, forms or polls
- [ ] Taken from other existing datasets
- [ ] Unknown

Source papers were retrieved and extracted from ACL Anthology; the codes themselves were generated by a language model, which is why both collection methods are selected.

**Data Sources**: ACL Anthology, https://aclanthology.org/ — Coverage 2020 to 2025, six venue tracks.

**Data Collection**

| | |
|---|---|
| Timeline | Dec 2025 – Aug 2026 |
| Data Modality | Text Data |
| Annotations | Machine-generated by a large language model |
| Date of coding run | Apr 2026 – Jun 2026 |

## Inclusion Criteria / Exclusion Criteria / Data Processing

**Inclusion Criteria**
- Paper is indexed in the ACL Anthology.
- Published between 2020 and 2025.
- Contains an identifiable Limitations section whose text could be extracted.
- Published in an ACL or EMNLP main or Findings track.

**Exclusion Criteria**
- Papers with no Limitations section, which cannot be coded.

**Data Processing**

Limitations sections were extracted from the source PDFs with the Python library `docling`.

The extracted text was segmented into semantic units by Gemini 2.5 Flash, prompted to preserve meaning rather than to split on orthographic sentence boundaries. The output was parsed into the sentence keys used here and was not manually corrected.

Each Limitations section was then coded against the codebook by a language model, which applied existing codes where they fit and, where none did, proposed new codes inductively.

## Sensitive Data / Fields with Sensitive Data / Security and Privacy Handling

**Sensitive Data**: [x] None

**Fields with Sensitive Data**: No field stores personal data directly. Indirect: `paper_id` resolves to a public paper with named authors, and the quoted sentences are that paper's own words.

**Security and Privacy Handling**: The source text is already public, so no de-identification was applied and none is required.

## Sensitive Human Attributes / Source(s) of Human Attributes / Rationale for Collecting Human Attributes

**Sensitive Human Attributes**: [x] None collected

**Source(s) of Human Attributes**: Not applicable. No human attribute was collected, labelled or derived.

**Rationale for Collecting Human Attributes**: Not applicable. The unit of analysis is a written statement, not a person.

## Transformations Applied / Libraries and Methods Used

- **PDF extraction**: `docling`
- **Segmentation**: Gemini 2.5 Flash, semantic units.
- **Coding model**: Gemini 3.1 Pro
- **Decoding**: temperature = 0

Segmentation and coding are the only transformations. No value in the released file was cleaned, imputed or type-converted after the coding run.

## Sampling Method(s) / Sampling Characteristic(s) / Sampling Criteria

**Sampling Method(s)**: [x] Unsampled

**Sampling Characteristic(s)**

| | |
|---|---|
| Population | ACL Anthology, 2020 to 2025 |
| Sample Size | 16,047 papers |

| Year | Papers | Breakdown |
|---|---|---|
| 2020 | 74 | acl-main 19, emnlp-main 37, findings-emnlp 18 |
| 2021 | 84 | emnlp-main 41, acl-long 24, findings-acl 8, findings-emnlp 9, acl-short 2 |
| 2022 | 1,437 | emnlp-main 817, findings-emnlp 528, acl-long 59, findings-acl 26, acl-short 7 |
| 2023 | 4,024 | findings-emnlp 1,044, emnlp-main 1,042, acl-long 897, findings-acl 885, acl-short 156 |
| 2024 | 4,159 | emnlp-main 1,266, findings-acl 967, findings-emnlp 997, acl-long 853, acl-short 76 |
| 2025 | 6,269 | emnlp-main 1,807, acl-long 1,591, findings-emnlp 1,397, findings-acl 1,378, acl-short 96 |

**Sampling Criteria**: N/A — unsampled; all qualifying papers were included.

## Annotation Workforce Type / Annotation Characteristics / Annotation Description

**Annotation Workforce Type**: [x] Machine-generated Annotations

**Annotation Characteristics**

| | |
|---|---|
| Code assignments | 84,930 |
| Evidence spans | 131,166 |
| Codes in the codebook | 50 |
| Limitation codes | 40 |
| Non-Limitation codes | 10 |
| Codes per paper | mean 5.29, range 1 to 19 |
| Spans per paper | mean 8.17, range 1 to 62 |
| Justification length | mean 115 characters, none empty |

**Annotation Description**

Each assignment ties a code to a paper and carries the evidence that produced it: the triggering sentence, a character span into the Limitations section, and a justification written by the model.

The codebook was revised annually as coding progressed, and every version is released alongside the data. The 50-code version documented here is the final one: 40 limitation codes and 10 Non-Limitation codes marking content that appears in a Limitations section without being a limitation.

Code frequencies are steeply skewed. *Non-Limitation: Future Work* appears in 12,041 papers and *Scope Limitation* in 10,091, while *Sparse Data Sensitivity* appears in 3 and *Dataset Task Mismatch* in 5, both surfaced as `new_code` before being formalised into `codebook_after_2025`.

## Annotator Breakdown / Annotator Description

**Annotator Breakdown**

| | |
|---|---|
| Annotator type | Language model |
| Model | Gemini 3.1 Pro |
| Human annotators | 0 |
| Assignments per paper | mean 5.29 |
| Working language | English |

**Annotator Description**

All coding was performed by a language model against the codebook. No human assigned, reviewed or adjudicated the labels in this dataset.

The codebook the model worked from was developed by the research team. Its first version was built from a pilot in which an LLM inductively coded 50 Limitations sections from ACL 2024 extracted with BAGELS (Al-Azher et al., 2025); those codes were manually aligned with the taxonomy of limitations in AI research of Xu et al. (2025) and extended to cover topics the pilot surfaced. It was revised iteratively thereafter, reaching the 50 codes documented here.

## Validation Method(s) / Validation Breakdown / Description of Validation

**Validation Method(s)**: [x] Data Type Validation · [x] Code/cross-reference Validation · [x] Structured Validation · [x] Others: inter-annotator agreement with the model treated as a coder

**Validation Breakdown**

| | |
|---|---|
| `paper_id` | 16,047 unique, 0 duplicates |
| Code/codebook resolution | every code in every file resolves to that file's applicable codebook version |
| Alpha, human annotators | 0.644 |
| Alpha, human annotators plus the model | 0.647 |

**Description of Validation**

Structural checks were run programmatically over the released file: every code carries a unique identifier and name, identifiers run consecutively without gaps, every sentence key matches the paper it belongs to, and no justification is empty.

Coding quality was assessed by treating the model as an additional coder against the companion human-annotated dataset — a separate release of 150 papers double-coded by four human annotators — and recomputing Krippendorff's alpha, binary multi-label at paper level, over the papers common to both datasets. Alpha among the human annotators alone is 0.644. Adding the model as a coder gives 0.647. The model therefore does not behave as an outlier: introducing it does not degrade the reliability of the coder pool.

## ML Application(s)

A large language model produced every label in this dataset. It was not trained or fine-tuned for the task; it was prompted to apply an existing codebook and to return, for each assignment, the sentences that triggered it and a justification.

No model was trained on this dataset.

## Reflections on Data

**These labels are model output, not ground truth**

Every code in this dataset was assigned by a language model with no human verification. The justifications make each assignment inspectable, which is useful, but a fluent justification is not evidence that the assignment is correct. Where a claim needs a reference standard, the companion human-coded dataset of 150 papers exists for that purpose.

**Temporal coverage**

The dataset holds 74 papers from 2020 and 84 from 2021, against 6,269 from 2025. Under 1% of the data comes from the first two years. This partly reflects reality — ACL Rolling Review, the shared reviewing pipeline both ACL and EMNLP draw submissions from, began asking authors to discuss limitations when it launched in 2022, and made a dedicated Limitations section mandatory, with desk rejection for its absence, only from the December 2023 cycle onward — but it means any trend line drawn across the full range is dominated by the recent years.

**Evidence spans do not always resolve against the source text**

`highlight_start`, `highlight_end` and `highlight_text` are derived by parsing the model's own output, and the model occasionally returns a highlighted text that does not match the actual content at that position in the Limitations section, so the span cannot be resolved correctly. The defective-span rate is 1.47% overall (1,933 of 131,166). This does not affect the code assigned or its justification, only the character span. However, each evidence entry also carries `segmented_id` and `segmented`, which identify the sentence-level unit the span was drawn from independently of the character offsets; where a span fails to resolve, the segment it points to still can, and remains usable for checking the evidence behind a code.

---

Structure follows the [Data Cards Playbook](https://sites.research.google/datacardsplaybook/) by Google Research, licensed under CC BY-SA 4.0.
