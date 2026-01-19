# BSB Bible Data

Auto-generated Bible data files from the Berean Standard Bible with Strong's numbers,
cross-references, topics, and morphology.

> **Note:** Do not edit these files directly. They are rebuilt automatically from
> source data by the bsb-data build pipeline.

## Directory Structure

```
.
├── base/                    # Core data files
│   ├── display/             # Per-book JSONL for web rendering
│   │   └── {BOOK}.jsonl     # e.g., GEN.jsonl, MAT.jsonl
│   ├── index-pd/            # Vector DB index (Public Domain)
│   │   └── bible-index.jsonl
│   └── index-cc-by/         # Vector DB index with morphology (CC-BY 4.0)
│       └── bible-index.jsonl
├── schema/                  # JSON schemas for all formats
│   ├── display.schema.json
│   ├── index-pd.schema.json
│   ├── index-cc-by.schema.json
│   └── book-codes.schema.json
├── VERSION.json             # Source versions and build date
└── README.md                # This file
```

## Licenses

| Directory | License | Attribution Required |
|-----------|---------|---------------------|
| `base/display/` | CC0 (Public Domain) | No |
| `base/index-pd/` | CC0 (Public Domain) | No |
| `base/index-cc-by/` | CC-BY 4.0 | **Yes** |
| `schema/` | CC0 (Public Domain) | No |

### CC-BY Attribution (required for index-cc-by)

When using `base/index-cc-by/` data, include this attribution:

> Hebrew morphology data from [Open Scriptures Hebrew Bible (OSHB)](https://hb.openscriptures.org/),
> licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).

## Data Formats

### Display Format (`base/display/*.jsonl`)

Compact format optimized for web rendering:

```json
{"b":"GEN","c":1,"v":1,"w":[["In the beginning","H7225"],["God","H430"],["created","H1254"],["the heavens","H8064"],["and","H853"],["the earth","H776"],[".",null]]}
```

### Index Format (`base/index-pd/bible-index.jsonl`)

Enriched format for vector DB indexing:

```json
{
  "id": "GEN.1.1",
  "b": "GEN",
  "c": 1,
  "v": 1,
  "t": "In the beginning God created the heavens and the earth.",
  "s": ["H7225", "H430", "H1254", "H8064", "H853", "H776"],
  "x": ["JHN.1.1", "HEB.11.3", "PSA.33.6"],
  "tp": ["Creation", "God, Creator"],
  "g": {"H7225": "beginning", "H430": "God", "H1254": "to create"}
}
```

### Index Format with Morphology (`base/index-cc-by/bible-index.jsonl`)

Same as index-pd plus morphology data:

```json
{
  "...all index-pd fields...",
  "m": [
    {"s": "H7225", "m": "HR/Ncfsa", "p": "noun", "l": "רֵאשִׁית"},
    {"s": "H430", "m": "HNcmpa", "p": "noun", "l": "אֱלֹהִים"}
  ]
}
```

## For Downstream Projects

This data is designed to be extended. To add your own enrichments:

1. Fork or clone this repository
2. Read from `base/` directories
3. Write your enhanced data to a new directory (e.g., `enhanced/`)
4. The schemas allow `additionalProperties` for custom fields

Example structure for an enhanced project:

```
your-project/
├── bsb-data-output/          # This repo as submodule
│   └── base/
├── scripts/
│   └── enhance.py            # Your enrichment code
└── enhanced/
    └── bible-enhanced.jsonl  # Your output with added fields
```

## Version Info

See [VERSION.json](VERSION.json) for source commit SHAs and build timestamp.

## Source Repositories

- **BSB-USJ:** https://github.com/BSB-publishing/bsb2usfm
- **Bible Databases:** https://github.com/scrollmapper/bible_databases
- **OSHB:** https://github.com/openscriptures/morphhb
