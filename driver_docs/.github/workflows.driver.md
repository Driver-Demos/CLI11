
## Files
- **[build.yml](workflows/build.yml.driver.md)**: The `build.yml` file in the `CLI11` codebase defines a GitHub Actions workflow for building and packaging the project, including generating a single header file and creating a release upon tagging.
- **[docs.yml](workflows/docs.yml.driver.md)**: The `docs.yml` file in the `CLI11` codebase defines a GitHub Actions workflow for generating and deploying API documentation and a GitBook to GitHub Pages upon pushes to the main branch, pull requests, or manual dispatches.
- **[fuzz.yml](workflows/fuzz.yml.driver.md)**: The `fuzz.yml` file in the `CLI11` codebase defines a GitHub Actions workflow for running fuzz testing on the main branch and pull requests, using Clang with specific configurations and uploading artifacts on failure.
- **[pr_merged.yml](workflows/pr_merged.yml.driver.md)**: The `pr_merged.yml` file in the `CLI11` codebase defines a GitHub Actions workflow that labels pull requests as "Changelog needed" when they are merged.
- **[tests.yml](workflows/tests.yml.driver.md)**: The `tests.yml` file in the `CLI11` codebase defines a GitHub Actions workflow for running various tests and builds, including coverage, Catch2, Clang-Tidy, CUDA, Boost, Meson, Bazel, and CMake configuration checks across different environments and configurations.
