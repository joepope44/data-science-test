# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

AI-generated data science project for testing Claude and agentic AI capabilities on real-world marketing problems. Uses `uv` as the package manager.

## Commands

- **Run the project:** `uv run main.py`
- **Add a dependency:** `uv add <package>`
- **Run a script:** `uv run python src/<script>.py`
- **Sync dependencies:** `uv sync`

## Project Structure

- `src/` - Source code for analysis scripts and modules
- `data/` - Input datasets
- `figures/` - Generated plots and visualizations
- `tables/` - Generated tabular outputs
- `main.py` - Entry point

## Dataset

Download the credit card customer attrition dataset from Kaggle:

```python
import kagglehub

# Download latest version
path = kagglehub.dataset_download("thedevastator/predicting-credit-card-customer-attrition-with-m")

print("Path to dataset files:", path)
```

## Dependencies

Python 3.9 with pandas, numpy, and matplotlib. Managed via `uv` with `pyproject.toml` and `uv.lock`.
