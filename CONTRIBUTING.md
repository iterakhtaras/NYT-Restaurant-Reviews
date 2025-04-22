# Contributing Guidelines

Thank you for your interest in contributing to the NYT Top‑100 Restaurant Reviews Analysis! Please follow these guidelines to help us maintain a consistent and high-quality codebase.

## Code Formatting
- **Language:** Python 3.9+
- **Style Guide:** Follow [PEP 8](https://www.python.org/dev/peps/pep-0008/) for Python code.
- **Linting:** Run `flake8` and `black --check .` before submitting changes.
- **Notebook Clean‑Up:** Clear all output cells in Jupyter notebooks before committing.

## Branch Strategy
- **Main Branch:** `main` holds production‑ready code; direct pushes are restricted.
- **Development Branch:** `develop` integrates features before release; merges into `main` happen via pull requests after review.
- **Feature Branches:** Prefix with `feature/`, e.g., `feature/add-sentiment-analysis`.
- **Hotfix Branches:** Prefix with `hotfix/`, e.g., `hotfix/fix-bug-123`.

## Pull‑Request Workflow
1. **Create Branch:** Base it off the `develop` branch.
2. **Implement & Test:** Ensure all tests pass (`pytest`) and notebooks run cleanly.
3. **Commit Messages:** Use imperative, present‑tense commits, e.g., “Add data validation for census loader”.
4. **Open a PR:** Target the `develop` branch. Include a clear title and description of changes.
5. **Review:** Assign at least one reviewer. Address comments and update the branch as needed.
6. **Merge:** After approval and passing CI, merge into `develop`. For releases, merge `develop` into `main` and tag a new version.

## Issues
- File new issues for bugs or feature requests, labeling them appropriately (e.g., `bug`, `enhancement`).

Thank you for helping improve this project!
