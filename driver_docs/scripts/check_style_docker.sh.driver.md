# Purpose
This script is a shell script designed to automate the process of formatting C++ source code files using a specific version of the ClangFormat tool within a Docker container. It provides narrow functionality focused on code formatting and is not intended to be a standalone executable or a library file. The script sets up a Docker environment to run the ClangFormat tool, specifying the Docker image version to use, and applies formatting rules defined in a configuration file to all C++ source files in the current directory. Additionally, it checks for any differences in the code after formatting by using `git diff`, ensuring that the codebase adheres to the specified style guidelines. This script is typically used in development environments to maintain consistent code style across a project.
# Global Variables

---
### CLANG\_FORMAT
- **Type**: `string`
- **Description**: The `CLANG_FORMAT` variable is a string that specifies the Docker image for the clang-format tool, set to 'saschpe/clang-format:5.0.1'. This variable is used to define which version of the clang-format tool will be used for formatting C++ code within a Docker container.
- **Use**: This variable is used to specify the Docker image for running the clang-format tool in subsequent Docker commands.


