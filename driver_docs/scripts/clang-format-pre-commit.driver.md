# Purpose
This Bash script is designed to serve as a Git pre-commit hook that automatically formats source code files using `clang-format`. It provides a narrow functionality focused on ensuring code style consistency for specific file types, such as `.hpp`, `.cpp`, `.c`, `.cc`, `.cu`, and `.h`. The script checks for any staged changes in these files and applies the formatting rules defined in a `.clang-format` configuration file. If any changes are made by the formatter, the script stages the updated files for commit. This script is not an executable or a library but rather a utility script intended to be linked into a Git repository's hooks directory to enforce code formatting standards automatically during the commit process.
# Functions

---
### format\_file
The `format_file` function formats C/C++ source files using clang-format and stages them for commit if changes are made.
- **Inputs**:
    - `file`: A string representing the file path of the source file to be formatted.
- **Control Flow**:
    - The function takes a single argument, `file`, which is the path to a file.
    - It checks if the file has an extension that matches C/C++ source files (e.g., .hpp, .cpp, .c, .cc, .cu, .h).
    - If the file exists and matches one of the specified extensions, it runs `clang-format` on the file with specific options to format it in place, sort includes, and use the style defined in a configuration file.
    - After formatting, it checks if the file has been modified by comparing it to the staged version using `git diff-files`.
    - If the file is unchanged, it prints a message indicating the file is already formatted.
    - If the file has been modified, it stages the file for commit using `git add` and prints a message indicating the file has been reformatted.
- **Output**: The function does not return a value but prints messages to the console indicating whether the file was already formatted or has been reformatted and staged.


