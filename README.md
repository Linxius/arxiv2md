# arxiv2md

<div align="center">
  <img src="assets/image.png" alt="arxiv2md" width="400">

  **arXiv papers → clean Markdown. CLI and Python library.**

  [Report Bug](https://github.com/Linxius/arxiv2md/issues)
</div>

---

## Why?

[gitingest](https://gitingest.com) but for arXiv papers.

## How It Works

Instead of parsing PDFs (slow, error-prone), arxiv2md parses the structured HTML that arXiv provides for newer papers. This means clean section boundaries, proper math (MathML → LaTeX), reliable tables, and fast processing — no OCR needed.

## Usage

### CLI

```bash
# Install from git repository
pip install git+https://github.com/Linxius/arxiv2md.git

# Basic usage
arxiv2md 2501.11120v1 -o paper.md

# Only extract specific sections
arxiv2md 2501.11120v1 --section-filter-mode include --sections "Abstract,Introduction" -o -

# Strip references and TOC
arxiv2md 2501.11120v1 --remove-refs --remove-toc -o -

# Include YAML frontmatter with paper metadata
arxiv2md 2501.11120v1 --frontmatter -o paper.md
```

### Python Library

```python
from arxiv2md import ingest_paper_sync

result = ingest_paper_sync("2501.11120v1")
print(result.content)

# or use the async version
from arxiv2md import ingest_paper

result = await ingest_paper("2501.11120v1")
```

Both accept the same optional keyword arguments:

| Argument | Default | Description |
|----------|---------|-------------|
| `remove_refs` | `True` | Remove bibliography/references sections |
| `remove_toc` | `True` | Remove table of contents |
| `remove_inline_citations` | `True` | Remove inline citation text |
| `section_filter_mode` | `"exclude"` | `"include"` or `"exclude"` for section filtering |
| `sections` | `None` (all) | List of section titles to include/exclude |
| `include_frontmatter` | `False` | Prepend YAML frontmatter with paper metadata |

## Development

```bash
# Clone and install in editable mode
git clone https://github.com/Linxius/arxiv2md.git
cd arxiv2md
pip install -e .[server]
uvicorn server.main:app --reload --app-dir src

# Run tests
pip install -e .[dev]
pytest tests
```

## Contributing

PRs welcome! Fork the repo, create a feature branch, add tests if applicable, and submit a PR.

## License

MIT

---