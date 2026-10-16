---
name: brand-extractor
description: Extract brand names and related metadata from a single website URL. Use this skill whenever a user wants to identify what brands are featured on a specific page, whether they are clothing, tech, or any other category.
---

# Brand Extractor Skill

This skill extracts brand names from a provided website URL and organizes them into a structured format.

## Core Workflow

1.  **Receive URL**: The user provides a URL to analyze.
2.  **Analyze Content**: The agent uses the `brand_extraction` directive to orchestrate the extraction.
3.  **Execute Extraction**: The agent calls `extract_brands.py` to fetch and parse the page.
4.  **Format Output**: The results are presented as a structured list (defaulting to JSON or a Markdown table).

## How to use

When a user asks to "extract brands from [URL]", "tell me what brands are on this page", or "list the brands at [URL]", activate this skill and follow the [brand_extraction directive](file:///c:/Users/Booyaah/agtest/directives/brand_extraction.md).

## Output Expectations

By default, provide:
- **Brand Name**: The official name of the brand.
- **Source Context**: A brief snippet or note about where it was found (e.g., "Featured in header", "Listed in footer").
- **Brand URL** (Optional): If the brand has a specific landing page or link on the site.

## Dependencies

- Python with `requests` and `beautifulsoup4` (or similar) installed in the environment.
- Access to the `read_url_content` or `read_browser_page` tools.
