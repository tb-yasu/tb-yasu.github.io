---
layout: default
title: "Deep OpenReview Research | Yasuo Tabei"
---

<img src="/images/deepresearch.png" alt="Deep OpenReview Research" style="width:100%; height:auto; border-radius:12px;">

## What You'll Learn

- How to find truly relevant papers from thousands of accepted papers
- An overview of "deep paper analysis" that goes beyond traditional keyword search
- Concrete examples of AI-powered paper evaluation and review information utilization

## The Problem: Missing Important Research in a Sea of Papers

Major AI conferences accept an enormous number of papers each year:

- **NeurIPS 2025**: 5,290 papers
- **ICLR 2025**: 3,704 papers
- **ICML 2025**: 3,260 papers

These papers represent months or years of work by researchers worldwide, yet **most papers remain unread and buried** in reality.

**Limitations of Traditional Keyword Search:**

Researcher A is interested in "graph generation," but when an important paper is titled "latent space controlled molecular graph synthesis," simple keyword search may fail to find it.

Furthermore, OpenReview contains valuable information such as Meta Reviews and Decision Comments for each paper, but conventional search tools cannot fully utilize this rich data.

To address this problem, we developed **Deep OpenReview Research**.

## The Solution: Deep OpenReview Research

An AI-powered paper discovery and analysis agent targeting accepted papers on OpenReview. It combines OpenReview API with LLMs to automatically discover papers related to your research interests, rank them, and generate comprehensive reports.

### The Three Depths of "Deep"

**1. Semantic Search**
- Traditional: Exact keyword matching
- Deep OpenReview Research: LLM automatically generates synonyms (e.g., "graph generation" → "molecular graph synthesis" and dozens of related expressions), discovering papers missed due to terminology variations

**2. Deep Review Analysis**
- Traditional: Only titles and abstracts
- Deep OpenReview Research: Analyzes Meta Reviews, Decision Comments, review scores, and author responses to understand why papers were accepted

**3. Multi-axis Evaluation**
- Traditional: Evaluation based solely on relevance
- Deep OpenReview Research: Comprehensive evaluation across 4 dimensions (relevance, novelty, impact, practicality), enabling prioritization based on research objectives

## Key Features

### 1. Natural Language Research Interest Specification

Describe your research interests in natural language rather than keyword lists.

```bash
python run_deep_research.py \
  --venue NeurIPS --year 2025 \
  --research-description "I'm interested in graph generation and its applications to drug discovery"
```

### 2. 4-Axis LLM Evaluation

Evaluates papers from 4 perspectives in a single LLM call: relevance, novelty, impact, and practicality. This helps distinguish between "interesting but impractical papers" and "implementable but less novel papers."

### 3. Full Utilization of OpenReview Information

Analyzes Meta Reviews, Decision Comments, review scores, author responses, and presentation formats (Oral/Spotlight/Poster) to understand why papers were accepted.

### 4. Automatic Report Generation

Outputs all analysis results as Markdown-formatted reports that can be used as research notes.

## Use Cases

### Case 1: Molecular Graph Generation Research

```bash
python run_deep_research.py \
  --venue NeurIPS --year 2025 \
  --research-description "I'm interested in molecular graph generation and drug discovery applications"
```

**Result:** Extracts top 100 relevant papers from 5,290, performs LLM evaluation, and generates a ranked report of the top 50 most relevant papers.

### Case 2: LLM Efficiency Techniques Survey

```bash
python run_deep_research.py \
  --venue NeurIPS --year 2025 \
  --research-description "LLM quantization and inference acceleration techniques"
```

**Result:** Prioritizes practical, implementable technical papers through practicality-focused evaluation.

## Processing Flow

1. Extract research keywords from natural language
2. LLM automatically generates synonyms
3. Search papers using OpenReview API
4. Initial filtering by keyword matching
5. Multi-axis LLM evaluation of top k papers (default: 100)
6. Rank by final score and generate report

## Example Output Report

```markdown
# [Rank 1] MolGen: Controllable Molecular Graph Generation

**Scores**
- Final Score: 0.892
- Relevance: 0.950 | Novelty: 0.850 | Impact: 0.825 | Practicality: 0.850
- Average Review Score: 8.2/10

**AI Evaluation**
High relevance to both graph generation and drug discovery applications. 
Proposes a novel approach for controllable molecular generation using 
diffusion models...

**Decision Comment**
Significant contribution to molecular design. Oral presentation.

**Presentation Format**: Oral Presentation (top-tier paper)
```

## Tech Stack

Python 3.12+, LangGraph/LangChain, OpenAI GPT-4, OpenReview API

## Getting Started

```bash
git clone https://github.com/tb-yasu/deep-openreview-research.git
cd deep-openreview-research
python -m venv venv && source venv/bin/activate
pip install -r requirements.txt

# Set OpenAI API key in .env file
cp .env.example .env

# Fetch paper data (first time only, approximately 60-90 minutes depending on environment)
python fetch_all_papers.py --venue NeurIPS --year 2025

# Run
python run_deep_research.py \
  --venue NeurIPS --year 2025 \
  --research-description "Your research interests"
```

For detailed configuration options, see the [GitHub repository (English)](https://github.com/tb-yasu/deep-openreview-research).

Japanese version repository is available [here](https://github.com/tb-yasu/deep-openreview-research-ja).

## Comparison with Other Tools

Deep OpenReview Research differentiates itself through the following features:

**✓ Unique to Deep OpenReview Research**
- Automatic synonym generation
- Review information analysis (Meta Review, Decision Comment)
- Multi-axis evaluation (4 dimensions: relevance, novelty, impact, practicality)
- Acceptance rationale analysis
- Custom report generation

**△ Semantic Scholar**
- Only simple metrics (e.g., Highly Influential Citations)

**× Google Scholar / Semantic Scholar**
- Do not support the above features

The key strength of Deep OpenReview Research is its full utilization of the OpenReview API, analyzing deep information from the acceptance process such as Meta Reviews and Decision Comments.

## Application Scenarios

- **Literature Review**: Streamline related work surveys for paper writing
- **Technology Survey**: Discover papers emphasizing implementation feasibility
- **Research Trend Analysis**: Cross-year and cross-conference investigations
- **Paper Reading Group Selection**: Select papers based on presentation format (Oral/Spotlight)

## FAQ

**Q: What are the processing time and cost?**

A: For evaluating 100 papers with GPT-4o-mini, depending on prompt design, it is designed to operate in approximately 1-2 minutes at a cost of $0.05-0.1.

**Q: Can it be used offline?**

A: Paper data is cached locally, but API connection is required for LLM evaluation.

**Q: Which conferences are supported?**

A: Conferences using OpenReview such as NeurIPS, ICML, and ICLR.

**Q: How accurate are the evaluations?**

A: This tool is under active development, and quantitative validation of paper evaluation accuracy is a future task. Scoring methods are subject to discussion. We recommend using AI evaluation results as reference information and having human researchers make final judgments on critical research decisions.

## Summary

Finding truly relevant papers from thousands of accepted papers each year is challenging. Deep OpenReview Research addresses this problem through three key approaches:

1. **Expanded search scope through automatic synonym generation** - Prevents missing papers due to terminology variations
2. **Deep review analysis** - Understands why papers were accepted from Meta Reviews and Decision Comments
3. **Multi-axis prioritization** - Comprehensive evaluation across relevance, novelty, impact, and practicality

We aim to reduce paper survey time from days to minutes or tens of minutes.

**Note**: This tool is under active development, and quantitative validation of paper evaluation accuracy is a future task. Scoring methods are subject to discussion. We recommend using AI evaluation results as reference information and having human researchers make final judgments on critical research decisions.

---

## Links
- [GitHub Repository (English)](https://github.com/tb-yasu/deep-openreview-research)
- [GitHub Repository (Japanese)](https://github.com/tb-yasu/deep-openreview-research-ja)
- [License: CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/)
- Requirements: Python 3.12+, OpenAI API Key

For questions, please visit the GitHub Issues page of each repository.

