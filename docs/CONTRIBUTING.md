# Contributing to YOLO

Thank you for your interest in contributing to this project! We value your contributions and want to make the process as easy and enjoyable as possible. Below you will find the guidelines for contributing.

## Quick Links
- [Main README](../README.md)
- [License](../LICENSE)
- [Issue Tracker](https://github.com/WongKinYiu/yolov9mit/issues)
- [Pull Requests](https://github.com/WongKinYiu/yolov9mit/pulls)

## Testing and Formatting
We strive to maintain a high standard of quality in our codebase:
- **Testing:** We use `pytest` for testing. Please add tests for new code you create.
- **Formatting:** Our code follows a consistent style enforced by `isort` for imports sorting and `black` for code formatting. Run these tools to format your code before submitting a pull request.

## CI Workflows

All workflows live in `.github/workflows/`. The build and test logic is defined once in `_build-test.yaml` and shared across workflows.

| Workflow | Trigger | What it does |
|---|---|---|
| `pr-checks.yaml` | PR to `main` | Runs version check, then lint + test if it passes |
| `develop.yaml` | Push to `main` | Lint + test after merge |
| `release.yaml` | Push to `main` | Creates git tag and GitHub Release |
| `docs.yaml` | Push to `main` (docs changed) | Deploys docs to GitHub Pages |

### PR check order

```
PR opened
├── version-check        (fast gate, ~5s)
│     ✅ pass
│     └── build_and_test (lint + test)
│           ✅ pass → merge allowed
│           ❌ fail → merge blocked
```

Tests are skipped entirely if the version wasn't bumped — no CI minutes are wasted.

### After merge

```
PR merged to main
├── CI (develop.yaml)   → lint + test
└── release.yaml        → git tag + GitHub Release
```

## How to Contribute

### Proposing Enhancements
For feature requests or improvements, open an issue with:
- A clear title and description.
- Explain why this enhancement would be useful.
- Considerations or potential implementation details.

## Versioning and Releases

This project uses [Semantic Versioning](https://semver.org/) (`MAJOR.MINOR.PATCH`).

**Every PR to `main` must include a version bump** in `pyproject.toml`. A CI check will block merge if the version is unchanged.

Choose the bump type based on what your PR does:

| Change type | Command | Example |
|---|---|---|
| Bug fix or small improvement | `make bump-patch` | `0.1.0 → 0.1.1` |
| New feature (backwards-compatible) | `make bump-minor` | `0.1.0 → 0.2.0` |
| Breaking change | `make bump-major` | `0.1.0 → 1.0.0` |

You can also edit `version` in `pyproject.toml` directly if you prefer. Once the PR is merged, a GitHub Release and git tag are created automatically.

## Pull Request Checklist
Before sending your pull request, always check the following:
- The code follows the [Python style guide](https://www.python.org/dev/peps/pep-0008/).
- Code and files are well organized.
- All tests pass.
- New code is covered by tests.
- `version` in `pyproject.toml` has been bumped.
- We would be very happy if [gitmoji😆](https://www.npmjs.com/package/gitmoji-cli) could be used to assist the commit message💬!

## Code Review Process
Once you submit a PR, maintainers will review your work, suggest changes if necessary, and merge it once it’s approved. On merge, a release is created automatically from the version in `pyproject.toml`.

---

Your contributions are greatly appreciated and vital to the project's success!

Please feel free to contact [henrytsui000@gmail.com](mailto:henrytsui000@gmail.com)!
