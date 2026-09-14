# TyphoonNER

A Chinese named entity recognition dataset for typhoon disaster texts.
Anonymous data-only release candidate based on frozen B014 annotations.

## Dataset

| Split | Sentences | Entity mentions |
| --- | ---: | ---: |
| Train | 14,929 | 81,873 |
| Development | 1,827 | 10,267 |
| Test | 1,832 | 10,151 |
| Total | 18,588 | 102,291 |

The corpus covers 2,360 documents. Source categories are NEWS (9,725 sentences), GOV (7,470), and BULLETIN (1,393). Source types are preserved from B014 and describe collection categories, not necessarily the original publisher of quoted content.

## Files and format

`train.jsonl`, `dev.jsonl`, and `test.jsonl` are UTF-8 JSON Lines files, with one sentence record per line. Download the repository ZIP using GitHub's Code > Download ZIP, then extract it.

Each record contains:

- `sentence_id`: unique anonymous sentence identifier.
- `doc_id`: anonymous source-document identifier, shared across sentences from the same document.
- `source_type`: NEWS, GOV, or BULLETIN.
- `split`: train, dev, or test; use the supplied split without reshuffling.
- `text`: the frozen sentence string. Do not normalize or alter it before using offsets.
- `entities`: a list of `text`, `label`, `start`, and `end` objects.
- `split_group_id`: re-encoded historical grouping identifier.
- `rc3_split_group_id`: re-encoded final release grouping identifier.

Offsets are zero-based Unicode character indices with an exclusive end, not UTF-8 byte indices or model-token indices. Each mention must equal the slice of the sentence from start through end minus one. For the synthetic string `8月10日`, TIME spans [0,5).

The nine entity labels and boundary conventions are documented in [ANNOTATION_GUIDELINES.md](ANNOTATION_GUIDELINES.md). Aggregate counts are provided in [DATASET_STATISTICS.json](DATASET_STATISTICS.json). [SHA256SUMS.txt](SHA256SUMS.txt) identifies this exact package version.

## Evaluation and limitations

Use exact span-and-label entity-level micro precision, recall, and F1. Train on train, select settings on dev, and reserve test for final evaluation. This release contains data and documentation only, not model training or QC code.

Annotations were constructed with LLM assistance and quality control; they are not error-free independent human gold. A separate post-freeze 300-sentence adjudicated audit reported precision 96.15%, recall 85.46%, and F1 90.49%. Those are audit estimates, not per-sentence guarantees. Class imbalance and residual boundary, label, and omission errors remain limitations.

## Packaging and provenance

Sentence strings, entity lists, record order, and split assignments are unchanged from B014. Sentence, document, and grouping IDs have been replaced consistently by neutral IDs. Internal dataset-origin fields have been omitted. This transformation does not remove people or organizations mentioned in source text. No code, author account links, private ID mapping, or experiment logs are included.

Original article URLs are not present in the frozen sentence files; this package does not claim complete source-URL provenance. It is a technical release candidate, not a certification of publication permission. See [DATA_USE.md](DATA_USE.md) before public redistribution.
