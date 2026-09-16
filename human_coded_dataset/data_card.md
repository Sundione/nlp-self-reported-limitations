# NLP Limitations with Human Qualitative Coding — Data Card

**Data Card Authors:** Tawan Thaepprasit

The formatted, original version of this data card is available as [`data_card.pdf`](data_card.pdf). This file mirrors that PDF in Markdown.

This dataset is associated with an EMNLP 2026 Findings paper, titled *["What Limits Us? Analyzing Self-Reported Limitations in NLP Research"](https://arxiv.org/abs/2609.15191)*. The dataset contains 150 papers sampled from the ACL Anthology published between 2020 and 2025. Each record holds the paper identifier, title, abstract, the verbatim Limitations section, and that section split into numbered sentences. Two layers of human qualitative codes are attached: codes drawn from an established codebook, and codes the annotators created where no existing code fitted the statement. It was built as a human reference standard for hybrid qualitative coding of limitation statements in NLP research. It is released together with the codebook the annotators used.

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
| Size of dataset | 0.50 MB |
| Number of instances | 150 |
| Number of fields | 7 |
| Number of labels | 606 |
| Average labels per instance | 4.04 |
| Algorithmic labels | 0 |
| Human labels | 606 |
| Segmented sentences | 1,036 |

Labeled classes is the union of the 24 codebook codes actually applied and the 25 distinct annotator-created codes. The released codebook holds 25 codes; one is never used in this sample and is retained so the document matches the instrument the annotators worked from.

**Description of Content**

One data point is a single published NLP paper: bibliographic context, the verbatim Limitations section, that section segmented into numbered sentences, and the qualitative codes assigned to it in two lists.

By venue: Findings of ACL (41), EMNLP main (25), Findings of EMNLP (25), ACL long (24), ACL short (13), ACL main (7), other tracks including workshops and demos (15).

## Dataset Subject / Example Data Point / Data Fields

**Dataset Subject**
- [ ] Sensitive Data about people
- [ ] Non-Sensitive Data about people
- [ ] Data about natural phenomena
- [ ] Data about places and objects
- [ ] Synthetically generated data
- [ ] Data about systems or products
- [x] Others: text published in academic proceedings
- [ ] Unknown

**Example: Data Point**

```
paper_id        2025.acl-long.2
title           GraphNarrator: Generating Textual Explanations for Graph Neural Networks
limitation      "The backbone of GraphNarrator is based on LLMs, which may be more costly
                to do inference than saliency-based explanation methods. …"
segmented_text  2 sentences, keyed _s01 and _s02
existing_code   ['High Financial Cost', 'High Time Consumption']
new_code        []
```

**Data Fields**

| Field | Type | Description |
|---|---|---|
| `paper_id` | str | ACL Anthology identifier, unique per record |
| `title` | str | paper title as published |
| `abstract` | str | paper abstract as published |
| `limitation` | str | verbatim Limitations section, 215 to 4,922 characters |
| `segmented_text` | str → dict[str, str] | JSON-encoded map of sentence identifiers to sentences, 1 to 37 entries per record |
| `existing_code` | str → list[str] | codes from the codebook, 535 labels across 24 distinct codes, 1 to 10 per record |
| `new_code` | str → list[str] | codes created where no codebook entry fitted, 71 labels across 25 distinct codes, 0 to 3 per record, empty for 99 records |

## Dataset Purpose(s) / Key Domains or Application(s)

**Dataset Purpose(s)**
- [ ] Monitoring
- [x] Research
- [ ] Production
- [ ] Others

**Domains**: Natural language processing, qualitative coding methodology, meta-research on scholarly writing.

**Problem Space**: Whether limitation statements in NLP papers can be coded consistently against a fixed qualitative codebook, and where that codebook proves insufficient.

## Dataset Usage / Intended and/or Suitable Use Case(s)

- [ ] Safe for production use
- [x] Safe for research use
- [ ] Conditional use
- [ ] Only approved use
- [ ] Others

- An evaluation set for scoring an automated coding pipeline.
- Methodological research on how limitation statements are written.
- Codebook revision, using `new_code` to identify statements the codebook could not accommodate.

Unsuitable for judging research quality, for claims about NLP as a field, or for supervised training at this size.

## Safety of Use with Other Data / Acceptable Transformations

- [x] Safe to use with other data
- [ ] Conditionally safe to use with other data
- [ ] Should not be used with other data
- [ ] Unknown

Acceptable transformations: [x] Joining with other datasets · [x] Subsampling and splitting · [x] Filtering · [x] Joining input sources · [x] Cleaning missing values · [x] Anomaly detection · [x] Grouping and summarizing · [x] Scaling and reducing · [x] Statistical transformations · [x] Redaction or Anonymization · [ ] Others

## Version Status / Dataset Version / Maintenance Plan

- [ ] Regularly Updated
- [ ] Actively Maintained
- [x] Limited Maintenance
- [ ] Deprecated

| | |
|---|---|
| Current Version | 1.0 |
| Last Updated | 08/2026 |
| Release Date | 08/2026 |

Maintenance plan: The dataset is a fixed reference standard. No expansion or ongoing support is planned.

## Access Policy / Retention Policy / Wipeout Policy

**Access Policy**: Public. The dataset and the codebook are released in the same GitHub repository under CC BY 4.0.

Repository: https://github.com/Sundione/nlp-self-reported-limitations

CC BY 4.0 follows ACL Anthology practice for material published from 2016 onward; all 150 papers fall in 2020 to 2025 across ACL-sponsored venues. Attribution to the original paper authors is required for the verbatim text and is carried by `paper_id`.

**Retention Policy**: No retention limit. The dataset is intended to remain available as a fixed reference, and contains no personal data.

**Wipeout Policy**: Not applicable. No deletion schedule applies.

## Data Collection Methods / Data Sources / Data Collection

**Data Collection Methods**
- [x] API
- [ ] Artificially Generated
- [ ] Crowdsourced – Paid
- [ ] Crowdsourced – Volunteer
- [ ] Vendor Collection Efforts
- [x] Scraped or Crawled
- [ ] Survey, forms or polls
- [ ] Taken from other existing datasets
- [ ] Unknown

**Data Sources**: ACL Anthology, https://aclanthology.org/ — Coverage 2020 to 2025, 15 venue tracks.

**Data Collection**

| | |
|---|---|
| Timeline | Dec 2025 – Aug 2026 |
| Data Modality | Text Data |
| Annotations | Human annotation by the research team, four annotators |
| Date of Annotation | Dec 2025 – Apr 2026 |
| Instrumentation | spreadsheet |

## Inclusion Criteria / Exclusion Criteria / Data Processing

**Inclusion Criteria**
- Paper is indexed in the ACL Anthology.
- Published between 2020 and 2025.
- Contains an identifiable Limitations section whose text could be extracted.

**Exclusion Criteria**
- Papers with no Limitations section, which cannot be coded.

**Data Processing**

Limitations sections were extracted from the source PDFs with the Python library `docling`. Only `title`, `abstract` and `limitation` were retained; the rest of the paper body was not collected.

The extracted text was segmented into numbered sentences keyed `paper_id_sNN` and stored as JSON, giving 1,036 sentences in total, 2 to 37 per paper. No cleaning, imputation, redaction or type conversion was applied.

Sentence segmentation was performed by Gemini 2.5 Flash, prompted to split each Limitations section into semantic units that preserve the meaning of the original rather than into orthographic sentences. The model output was parsed into the JSON structure stored in `segmented_text` and was not manually corrected.

## Sensitive Data / Fields with Sensitive Data / Security and Privacy Handling

**Sensitive Data**: [x] None

**Fields with Sensitive Data**: No field stores personal data directly, and annotator identity is not recorded. Indirect: `paper_id` and `title` resolve to a public paper with named authors.

**Security and Privacy Handling**: The source text is already public, so no de-identification was applied and none is required.

## Sensitive Human Attributes / Source(s) of Human Attributes / Rationale for Collecting Human Attributes

**Sensitive Human Attributes**: [x] None collected (Race, Gender, Ethnicity, Socio-economic status, Geography, Language, Sexual Orientation, Religion, Age, Culture, Disability, Experience or Seniority — none of these were collected)

**Source(s) of Human Attributes**: Not applicable. No human attribute was collected, labelled or derived, for paper authors or for annotators.

**Rationale for Collecting Human Attributes**: Not applicable for the data itself. The unit of analysis is a written statement, not a person. Annotator background does shape coding decisions on interpretive categories; that is addressed under Annotator Breakdown and Validation below.

## Transformations Applied / Libraries and Methods Used

- [x] Others: sentence segmentation of the Limitations section

- **PDF extraction**: `docling`
- **Sentence segmentation**: Gemini 2.5 Flash, prompted to segment semantic units; output parsed into JSON, not manually corrected.
- Segmentation produced 1,036 units across 150 papers, a mean of 6.91 per paper, ranging from 2 to 37. The join is on `paper_id` and alters no values.

## Sampling Method(s) / Sampling Characteristic(s) / Sampling Criteria

**Sampling Method(s)**: [x] Random Sampling

**Sampling Characteristic(s)**

| | |
|---|---|
| Population | ACL Anthology, 2020 to 2025 |
| Sample Size | 150 papers |

The realised sample is uneven by year, with 68 of 150 drawn from 2024.

**Sampling Criteria**: The 150 papers were drawn in two stages. The first 50 were sampled at random from ACL 2024 alone and restricted to Limitations sections shorter than 500 characters, before the scope of the study was fixed. The remaining 100 were sampled at random across the full 2020 to 2025 range.

## Annotation Workforce Type / Annotation Characteristics / Annotation Description

**Annotation Workforce Type**: [x] Human Annotations – Expert

**Annotation Characteristics**

| | |
|---|---|
| Total annotations | 606 |
| From the codebook | 535 |
| Created by annotators | 71 |
| Distinct codes applied | 24 codebook, 25 created |
| Papers with ≥1 created code | 51 of 150 |
| Mean labels per paper | 4.04 |
| Annotators per paper | 1–3 |

**Annotation Description**: Each paper receives two lists. `existing_code` holds codes drawn from the codebook; `new_code` holds codes the annotator created because no codebook entry fitted. Every label resolves to an entry in the released codebook. The codebook holds 25 codes, 18 describing substantive limitations and 7 marking non-limitation content such as future work or reported strengths.

## Annotator Breakdown / Annotator Description

**Annotator Breakdown**

| | |
|---|---|
| Annotator type | Expert |
| Total unique annotators | 4 |
| Annotators per paper | 2–3 |
| Expertise | NLP research background |
| Working language | English |

**Annotator Description**

The codebook was built from a pilot in which an LLM inductively coded 50 Limitations sections from ACL 2024 extracted with BAGELS (Al Azher et al., 2025). Those empirical codes were manually aligned with the taxonomy of limitations in AI research of Xu et al. (2025), which was extended to accommodate novel topics observed in the pilot. Codes for non-limitation content such as future work, method strengths and conducted mitigation were added to support the analysis of rhetorical strategies.

The codebook is released alongside the dataset as [`codebook_initial.csv`](codebook_initial.csv).

Coding proceeded in two phases. In a calibration phase, the annotators independently coded a shared set of papers and then met to resolve every disagreement, using those discussions to align their reading of the codebook. In the main phase, each paper was independently coded by at least two annotators, and disagreements were resolved paper by paper in consensus meetings rather than by majority vote or by a single adjudicator.

The labels released in `existing_code` and `new_code` are the post-consensus result. Inter-annotator agreement is computed on the independent codings before consensus.

**References**

- Ibrahim Al Azher, Miftahul Jannat Mokarrama, Zhishuai Guo, Sagnik Ray Choudhury, and Hamed Alhoori. 2025. BAGELS: Benchmarking the Automated Generation and Extraction of Limitations from Scholarly Text. In *Findings of the Association for Computational Linguistics: EMNLP 2025*, pages 19279–19294, Suzhou, China. Association for Computational Linguistics.
- Zhijian Xu, Yilun Zhao, Manasi Patwardhan, Lovekesh Vig, and Arman Cohan. 2025. Can LLMs Identify Critical Limitations within Scientific Research? A Systematic Evaluation on AI Research Papers. In *Proceedings of the 63rd Annual Meeting of the Association for Computational Linguistics (Volume 1: Long Papers)*, pages 20652–20706, Vienna, Austria. Association for Computational Linguistics.

## Validation Method(s) / Validation Breakdown / Description of Validation

**Validation Method(s)**: [x] Code/cross-reference Validation · [x] Structured Validation · [x] Consistency Validation

**Validation Breakdown**

| | |
|---|---|
| Records checked | 150 |
| `paper_id` | 150 unique, 0 duplicates |
| All seven fields | 0 missing values |
| Label resolution | 606 of 606 resolve to a codebook entry |
| Inter-annotator agreement | 0.644 |

**Description of Validation**: Structural checks were run programmatically over the released file: every row parsed, no identifier repeated, no field empty, and every label matched against the codebook. Inter-annotator agreement was computed as Krippendorff's alpha under a binary multi-label formulation, in which each code is treated as a separate present-or-absent decision and agreement is pooled across codes.

## Validators Characteristic(s) / Validators Description(s)

N/A (automatic validation)

## ML Application(s)

No model was trained or fine-tuned on this dataset. It was used to evaluate the coding reliability of the LLM pipeline.

## Reflections on Data

**Coding is interpretive, and the dataset records where it broke down**

Assigning a code to a limitation statement is a judgement, not a measurement. The same sentence can support more than one reading, and 51 of the 150 papers required codes the codebook did not contain. That column was kept separate rather than merged into the existing codes precisely so the gaps stay visible.

---

Structure follows the [Data Cards Playbook](https://sites.research.google/datacardsplaybook/) by Google Research, licensed under CC BY-SA 4.0.
