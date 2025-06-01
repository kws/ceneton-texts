# Ceneton Transcript Archive

This repository contains an archival copy of the Ceneton transcripts: a comprehensive census of Dutch-language theatrical works up to the year 1803. Developed and maintained by the Department of Dutch at Leiden University, Ceneton ("Census Nederlands Toneel") is a major scholarly resource documenting over 12,500 plays, including metadata, bibliographic details, and textual editions. The original datasource is available at https://www.let.leidenuniv.nl/Dutch/Ceneton/.

The purpose of this repository is to add unique and immutable IDs and version control to the transcripts to make them easier to reference.

Some typos and broken links on the original website are corrected. These are tracked in the [extras](./extras) folder.

This URL list is built from the [ceneton-database](https://github.com/kws/ceneton-database) repository.

The code and utilities for maintining the archive are in the [ceneton-texts-utils](https://github.com/kws/ceneton-texts-utils) repository.

## Archive Structure

This repository maintains a structured archive with the following organization:

### index.csv

The `index.csv` file serves as the master catalog for all downloaded texts. It contains:

- **text_id**: Unique numeric identifier for each text (starting from 1)
- **url**: The original URL from the Ceneton website
- **source_slug**: Slug indicating the source with prefix (`ceneton:` or mapping file)
- **skip**: Boolean flag to indicate texts that should be skipped
- **original_slug**: Original slug from the source (when different from current)
- **last_status**: HTTP status code from the last download attempt
- **last_checked**: Timestamp of the last download check
- **comments**: User comments about the entry

### Download Folder Structure

Downloaded texts are organized in a hierarchical structure to avoid having too many folders in a single directory:

```text
archive/
├── index.csv
├── 0000-0100/
│   ├── 0001/
│   │   ├── metadata.yml
│   │   └── content.html
│   ├── 0002/
│   │   ├── metadata.yml
│   │   └── content.html
│   └── ... (more numbered folders)
├── 0100-0200/
│   ├── 0100/
│   │   ├── metadata.yml
│   │   └── content.html
│   └── ... (more numbered folders)
└── ... (additional hundred-range folders)
```

Each text folder contains:

- **metadata.yml**: Download metadata including timestamps, ETags, and content hashes

- **content.html**: The actual HTML content of the text

- **content.txt**: Extracted plain text from the HTML content using `w3m`.

### index-ceneton.csv

The `index-ceneton.csv` file links the original Ceneton database entries to the downloaded texts after best efforts to resolve the correct files. This mapping enables:

- Cross-referencing between the original Ceneton numbering system and our immutable text_id system
- Tracking which Ceneton entries correspond to successfully downloaded texts
- Preserving the original bibliographic metadata (author, title, year, genre, etc.) alongside the archived content

The file contains columns like `nummer` (original Ceneton ID), `text_id` (our archive ID), `auteurva`, `titel`, `jaarnr`, `genre`, and publication details.

## Mapping Files

The [extras/mappings](./extras/mappings) folder contains correction files that track modifications made to improve the archive:

### corrected.csv

This file maps Ceneton slugs that contain typos or other minor issues to their corrected versions. For example:
- Fixing typos in filenames
- Standardizing naming conventions
- Resolving inconsistent slug formats

### redirects.csv

This file handles HTML files that have meta-refresh redirect tags, mapping the redirecting page to the actual target page. This ensures users are directed to the correct content rather than intermediate redirect pages.

## Acknowledgements

The Ceneton project was led by **A.J.E. Harmsen** at Leiden University. Ceneton has been supported by the Gratama Foundation and is cited in scholarly and journalistic work on Dutch literary digitization.

## License and Use

This archival dataset is provided for **academic and research use**. Attribution should be given to the original maintainers at Leiden University.

