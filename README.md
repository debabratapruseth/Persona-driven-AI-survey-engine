

# Persona-Driven Survey Engine (AI-Powered Product Discovery)

Build a synthetic focus group using large-scale persona data + LLMs to simulate user feedback and validate product ideas before real user testing.

⸻

## Problem

Early-stage product teams struggle to answer:

* Who is my real target user?
* What do they actually care about?
* Will they buy this product?

Traditional methods (surveys, interviews, market research) are:

* slow
* expensive
* unavailable in early stages

⸻

## Solution

This project builds a persona-driven survey pipeline:

Raw dataset → Filtered personas → Segmentation → Survey generation → Simulated responses → Insights

⸻

## Architecture

                ┌──────────────────────────┐
                │ Persona Dataset (1M+)    │
                │ (HuggingFace)            │
                └────────────┬─────────────┘
                             ↓
                ┌──────────────────────────┐
                │ Filtering + Scoring      │
                │ (Target Audience)        │
                └────────────┬─────────────┘
                             ↓
                ┌──────────────────────────┐
                │ Segmentation Engine      │
                │ (Behavioral Clusters)    │
                └────────────┬─────────────┘
                             ↓
                ┌──────────────────────────┐
                │ Persona Builder (LLM)    │
                │ Structured Personas      │
                └────────────┬─────────────┘
                             ↓
                ┌──────────────────────────┐
                │ Survey Generator (LLM)   │
                └────────────┬─────────────┘
                             ↓
                ┌──────────────────────────┐
                │ Response Simulator (LLM) │
                └────────────┬─────────────┘
                             ↓
                ┌──────────────────────────┐
                │ Insight Extraction (LLM) │
                └──────────────────────────┘

⸻

## Tech Stack

* Python (Colab / Jupyter)
* Hugging Face Datasets – data ingestion
* Pandas – data processing
* scikit-learn – clustering (optional)
* Sentence Transformers – embeddings (optional)
* OpenAI API – persona generation, survey, simulation
* JSON pipelines for intermediate artifacts

⸻

## Dataset

* Nemotron Personas USA
* ~1M synthetic personas
* Fields:
    * demographics (age, location, marital status)
    * occupation
    * hobbies, skills
    * free-text persona descriptions

⸻

## Pipeline Overview

1. Data Preparation

* Load subset (10k–50k rows)
* Clean nulls
* Create combined_text for NLP filtering

⸻

2. Target Audience Filtering

Example:

Parents of children aged 4–10

Since no explicit label:

* heuristic scoring using:
    * keywords (kids, family, school)
    * age band (25–50)
    * marital status

⸻

3. Behavioral Segmentation

Rule-based classification into:

* Security-first
* Growth-oriented
* Busy
* Budget-conscious
* Values-driven
* Skeptical

Based on keyword signals in persona text.

⸻

4. Persona Panel Selection

* Deduplicate personas
* Rank by relevance score
* Select 10–12 representative samples

→ Forms a synthetic focus group

⸻

5. Persona Generation (LLM)

Transform raw rows into structured personas:

{
  "name": "...",
  "segment": "...",
  "financial_mindset": "...",
  "pain_points": [],
  "purchase_triggers": [],
  "objections": []
}

⸻

6. Survey Generation (LLM)

* Persona-aware question generation
* Merge into master survey
* Structured into sections:
    * awareness
    * trust
    * pricing
    * usability
    * decision triggers

⸻

7. Response Simulation (LLM)

Each persona:

* answers all survey questions
* provides reasoning
* reflects segment-specific behavior

⸻

8. Insight Extraction (LLM)

Aggregate responses to extract:

* recurring needs
* objections
* segment preferences
* rejection drivers
* product opportunities

⸻

📊 Output Artifacts

* clean_financial_parent_personas.json
* financial_product_survey.json
* simulated_survey_responses.json
* insights.json

⸻

## Example Use Case

Product tested:
FlexiSave Kids Plan

* goal-based savings
* micro-investments
* financial learning for kids

Insights enabled:

* which segments trust the product
* key objections (risk, complexity)
* messaging improvements
* feature prioritization

⸻

## Key Design Decisions

* Heuristic filtering instead of strict labels
* Small persona panel (10–12) instead of full dataset
* LLM for structure, not raw generation
* Simulation before real validation

⸻

## Limitations

* Synthetic personas ≠ real users
* Bias from dataset + prompt design
* Requires real-world validation post-analysis

⸻

## Extensions

* Replace rule-based segmentation with clustering
* Add embedding-based persona similarity
* Build UI using Streamlit
* Integrate real survey responses for hybrid analysis
* Multi-product A/B simulation

⸻

## Summary

This system enables:

* rapid product validation
* persona-driven survey design
* simulated user feedback at scale

A practical way to move from idea → insight before building anything.

⸻

